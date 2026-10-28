# Migrating Quarterly Losses to Rust

Goal: ship the game as an optimised native executable (Windows first, then Linux and macOS) without a long freeze, and keep a browser build from the same code.

## Where the code is today

| | Size | What it means for a port |
|---|---|---|
| `src/game.html` | ~11,900 lines, ~510 functions, one file | Has to be split into modules before anything moves |
| Procedural art | ~2,950 `painter` calls (`P.r/P.p/P.ell/P.line`), ~500 `px()` calls, ~250 raw Canvas2D calls, 18 composite modes, pixel passes via `getImageData` (`postProcess`, `sculptHuman`, battle damage, burn frames) | The largest visual port. Most of it is integer rectangles and pixels, which port 1:1 |
| Rendering | A 396×234 world buffer drawn at 1 art pixel = 2 logical px, upscaled; a full-resolution light pass of additive radial gradients; baked ground, water and fire frames | Maps well to one framebuffer plus one additive light shader |
| UI | 43 HTML-templated screens, 54 click actions, ~460 lines of CSS (envoy calls, the desk, store, reviews, manager, settings) | The largest functional port: no HTML in a native window |
| Audio | A Web Audio synth: oscillators, filters, noise, a 16-step sequencer with per-world arrangements, faction themes and live layers | Small, self-contained, straightforward to port |
| Simulation | Missions (paths, waves, hordes, enemies, crew, perks, auras, raids), the run (acts, factions, envoys, standing, morale, the manager, endings) | The core worth having in Rust; must match the JS exactly |
| Randomness | ~330 uses of `rnd()` / `Math.random()`, unseeded | Blocks exact parity testing; fix first |
| Saves | JSON in `localStorage` (`al_run`, `al_settings`, `al_endings`, `al_colony`, `al_fallen`) | Keep the schema so saves carry across |

## Options

1. **Wrap it (Tauri 2).** A Rust shell around the existing game in the system webview (WebView2, which is Chromium, on Windows). An .exe in days, saves on disk, store-ready. Performance is the browser's. Low risk, but not "Rust" where it counts.
2. **Rewrite natively in one go.** Months with nothing shippable in between, and the game is still changing every week. High risk.
3. **Migrate in stages (recommended).** Ship the wrapper first, move the simulation into a Rust crate that also compiles to WebAssembly and runs inside the current page, prove it matches the JS tick for tick, then replace rendering, UI and audio one at a time. There's a playable build at every stage, and the browser version comes from the same Rust code at the end.

## Recommended stack

- **Window, input, GPU:** `macroquad` (small, 2D-first, builds to WASM). `wgpu` with `winit` and `pixels` is the fallback if we need tighter control. Bevy is more than this game needs.
- **Procedural sprites:** `tiny-skia`, whose fill, path, gradient and blend API is close to Canvas2D, so `painter`, `postProcess` and the building and portrait generators port almost line for line. Sprites are generated once and uploaded as textures.
- **Lighting:** one additive pass of radial-gradient quads in a small shader, replacing the per-light `createRadialGradient` calls.
- **UI:** `egui` with a custom skin matching the corporate-intranet look, and text moved into data files.
- **Audio:** `cpal` with a port of the synth (oscillator, envelope, filter, noise) and the sequencer; `fundsp` if we want ready-made DSP.
- **Data and saves:** `serde` with JSON (same save schema, so web saves import) and RON for the content tables.
- **Platform:** `steamworks-rs` later; GitHub Actions builds for Windows, Linux and macOS.

Crate layout:

```
crates/al-core    simulation, content tables, saves; no IO, deterministic, builds to native and WASM
crates/al-art     procedural sprites and baked ground/water/fire frames (tiny-skia)
crates/al-audio   synth and sequencer
crates/al-game    the app: macroquad window, renderer, egui screens, input
web/              the current JS game, shrinking as pieces move to Rust
data/             factions, enemies, perks, relics, text (RON/JSON, shared with the JS during the move)
```

## Stages

| Stage | Work | Done when | Rough size |
|---|---|---|---|
| 0. Prepare (JS) | Split `game.html` into modules (data, sim, art, ui, audio) with a build step; one seeded PRNG in place of every `Math.random`/`rnd`; content tables out to JSON; a replay recorder (seed + player inputs) and a per-tick state hash | Same game, now reproducible from a seed and an input log | 1–2 weeks |
| 1. Exe (Tauri) | Tauri 2 shell, saves in the user's app data folder, fullscreen and window settings, CI builds and an installer | A downloadable .exe of today's game | 2–4 days |
| 2. Rust core in WASM | `al-core`: run state, contracts, waves and hordes, enemies, crew and perks, combat, raids, saves. The page calls it through `wasm-bindgen`; JS keeps the drawing | Golden replays match the JS state hash every tick over full five-act runs | 3–6 weeks |
| 3. Native renderer | `al-art` and the renderer in `al-game`: world buffer, light shader, sprites, ground, water and fire, map, ship, planet scenes, portraits | A native window plays missions; the web/Tauri build stays the shipping build | 4–8 weeks |
| 4. UI | The 43 screens in egui: envoys, desk, store, reviews, manager, settings, endings | The native build plays a full run with no webview | 4–8 weeks |
| 5. Audio | Synth and sequencer in `al-audio`, through `cpal` natively and Web Audio in WASM | Music and effects match the reference recordings | 1–2 weeks |
| 6. Ship | Parity sweep, frame budget on low-end hardware, controller support, Steam, then retire the JS | The native .exe and the WASM web build both come from the Rust code | 2–4 weeks |

The total is roughly **4–7 months of focused work**, most of it in stages 3 and 4. Stage 1 alone answers "can it run as an exe" within days.

## Rules for the migration

- **The JS stays the reference until parity.** Each system moves only when its golden replays match. A mismatch is a bug in the port, not a balance change.
- **Freeze features system by system, not the whole game.** While combat is being ported, new combat features go into the JS and the port together, or wait.
- **Port the art pixel for pixel.** Prefer the integer `P.r`/`P.p` paths over anti-aliased shapes so sprites match exactly, and compare screenshots per biome, faction and building type (the existing Playwright sheets become the reference set).
- **Keep the frame budget.** The current stress test (160–190 hostiles, eight crew) becomes a native benchmark; the target is a steady 60 fps on integrated graphics.

## Risks

- **A moving target.** The game still changes weekly. Stage 0 (modules, data files, replays) makes ports cheap to keep in sync; skipping it makes everything after it slower.
- **Visual drift.** Canvas2D and tiny-skia rasterise ellipses and anti-aliased edges differently. Mitigation: integer-pixel helpers, and screenshot diffs per asset.
- **UI fidelity.** egui is not HTML; the intranet styling, desk and envoy layouts need careful skinning. If that proves too costly, the fallback is to keep a webview for menus only.
- **Expectations.** The game isn't CPU-bound today except in the heaviest fights; the exe is mostly about distribution, and Rust buys headroom for bigger hordes and effects.

## First steps

1. Seeded PRNG and replay recording in the current JS (also useful now, for reproducing tester bugs).
2. Split `game.html` into modules with a bundler, so the single-file build still comes out the other end.
3. Tauri 2 wrapper and CI, so testers get an .exe straight away.
4. Create `crates/al-core` and port the content tables and save schema first: no logic yet, just data that both builds read.
