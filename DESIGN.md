# Acceptable Losses: design notes

Satirical roguelite tower defence. You work for Kindly Security Solutions™, an immoral private
security company. You defend clients' crystal extractions across Earth and the galaxy.

## Core loop (vertical slice)
1. **Star map**: pick one of 3 contracts (planet bubbles). Each shows the client, whether they're good or bad people, the hostile faction, biome hazard, difficulty and pay.
2. **Mission** (about 2.5–4.5 min): procedurally generated map. Deploy crew next to the path and hold until the drill reaches 100%, then clear the area to evacuate.
3. **Debrief**: a satirical HR email plus a payslip in Company Scrip, with itemised deductions.
4. **Company Store**: hire crew, buy relics, promote crew, or use creative accounting to restore margin.
5. Repeat. Sector 1 is 4 contracts, then a boss. The boss faction is whichever faction you fought most.

## Rules
- **Profit margin** is run-wide HP (starts at 100%). Leaked enemies reduce it. At 0% you're abandoned and stranded.
- **Budget** is spent during a mission to deploy crew (from kills plus a trickle). **Scrip** is spent between missions, only at the store.
- **Crew** are named towers that carry over between contracts. They gain XP and promotions (a new title, no raise). Saboteurs can injure them for the rest of a contract.
- **Enemies**: 5 categories (Swarm, Runner, Armoured, Flyer, Saboteur) × 3 tiers (Grunt, Veteran, Elite), skinned by 4 factions.
- **Persistence**: factions you've fought return with a grudge (+10% HP). The boss is chosen from your history. Hints about the mind-control twist show up in email P.S. lines.
- **Meta**: every failed run adds a survivor to the Colony of the Abandoned (+5 starting scrip each, capped at 50).

## Art direction: neo-pixel
- The playfield is drawn into a low-res buffer (1 art px = 2 game px) and scaled up crisply. Lights, tracers, taser arcs, muzzle flashes and the laser sight are drawn on top at full resolution with additive glow.
- **Crew** are 12×17 chibi sprites. The body is random (10 skin tones, 12 hair styles including afro, braids, bun and headscarf, natural or dyed hair colours, facial hair, glasses, build, and extras like freckles, an eyepatch or a plaster). The role sets the outfit: hi-vis guard, taser tech with a battery pack, hard-hat mortar crew, pink-polo intern with a lanyard, hoodie drone operator. Everyone stands on a company-issued pallet.
- **Firing**: weapons track the target smoothly and kick back on recoil. Effects include muzzle flash sprites and light, ejected shell casings, gunner two-round bursts, taser arcs, foam mortar shells with smoke trails and foam splats, the marksman's charging laser sight and screen shake, and the drone's hover-and-tilt.
- **Enemies**: humans for the miner, protester and VectorCorp factions use the same random people generator with faction outfits and props. Each faction has its own vehicle (treads, van, walker) and drone. Wildlife are hand-built creature sprites. Veterans get a white outline and Elites a gold one.
- **Terrain**: per-biome noise ground, a path sunk below the ground, biome decorations, and obstacle sprites with their own light sources.

## Worlds
Seven trope worlds, each with its own ground and path palette, path treatment, ground decor, 5 obstacle types, 2x2 landmarks (1–3 per map), animated props, weather, a colour grade, and 2–3 planet colour schemes on the star map.

| World | Trope | Path | Obstacles | Landmarks | Weather | Planet schemes |
|---|---|---|---|---|---|---|
| Ice World | Classic ice planet | Packed snow with footprints | Ice shards, snow boulders, survey beacons, frozen ribcages, snowdrifts | Research dome | Snow | Ice Planet, Glacier World, Frost Giant Moon |
| Death World Jungle | Everything bites | Mud with puddles | Alien bulbs, carnivorous pitchers, glowing mushrooms, giant skulls, thorn bushes | Glowing alien tree | Spores | Death World Jungle, Fungal Planet, Acid Swamp |
| Desert Planet | Twin suns, sandworm skeletons | Rippled sand | Boulders, moisture vaporators, sandworm ribs, crashed pods, alien cacti | Crashed starship | Blowing sand | Twin-Sun Desert, Red Planet, Spice Dunes |
| Crystal Moon | Low-gravity crystal moon | Regolith with bootprints | Crystal rocks and spires, floating rocks, radar dishes, crater rims | Dish array | Floating motes | Crystal Moon, Grey Moon, Ringed Shard |
| **Neon Megacity** | Cyberpunk | Wet asphalt with neon kerbs and puddles | Vending machines, neon signs, dumpsters, AC units, holo kiosks, barriers | Holo billboard cycling ads | Rain | Ecumenopolis, Neon Sprawl |
| **Solarpunk Commune** | Solarpunk | Mossy stone pavers | Solar panels, planters, fruit trees, beehives, fountains | Wind turbine or garden tower | Pollen and butterflies | Garden World, Terraformed Paradise (gold solar rings) |
| Forge World | Lava hellscape | Basalt tiles with glowing cracks | Obsidian, lava pools, mining drills, basalt columns, steam vents | Ruined forge tower | Rising embers | Forge World, Hell Moon |

## Crew progression: performance reviews
Each promotion gives a small base boost (+10% damage, +3% fire rate, +12 HP per rank) and a **performance review** in which you pick a card. Reviews can be held mid-contract (click the highlighted crew card, or press R; the game pauses) or between contracts ("Hold performance reviews").

| Rank | Review | Options |
|---|---|---|
| 2 | Tier I · Common | 3 cards: role perks topped up with corporate perks |
| 3 | Tier II · Rare | 3 cards: mechanic changers (armour shred, multishot, cluster shells, executes, extra drones...) |
| 4 | Specialisation | 1 of 2 permanent branches per role, each showing its future capstone |
| 5 | Capstone | the branch capstone, or one of 2 Tier II cards |
| 6–8 | Executive | high-impact perks with trade-offs (Golden Handcuffs, Burnout Protocol, Stock Options...) |

- **Branches**: Turret Operator (Suppression Specialist / Hazard Pay Gunslinger), Taser Tech (Storm Caller / Crowd Control Officer), Mortar (Long-Range Artillery / Foam Containment), Marksman (Wetwork Contractor / Spotter), Drone Operator (Drone Swarm Manager / Field Medic).
- **Capstones** include map-wide lightning, freezing pulses, 5-shell barrages, damage-amplifying foam, executes that refund the reload, spreading marks, 4-drone hive minds, and a protective medic aura.
- **Quirks**: every hire rolls one of 10 traits (Nepotism Hire, Tenured, Office Gossip...). They're shown in the store before you hire.
- **Appeal decision** rerolls the cards for scrip (10, then +5 each time). **Decline promotion** takes 12 scrip instead.
- **Synergies**: marks (Tracer Rounds, Static Cling, Spotter, Quagmire foam) amplify all crew damage. Auras buff, heal or protect crew within 1.5 tiles.
- XP thresholds: 16 / 45 / 95 / 165 / 260 / 380 / 530.

## Audio
- Everything is synthesised live with Web Audio. There are no audio files. Audio starts on the first tap or key press, which is a browser rule.
- **Music**: a small chiptune sequencer with five tracks.
  - Corporate hold music on the menus, mail and store.
  - Drifting arpeggios on the star map.
  - A driving mission loop that adds layers as the drill fills.
  - A faster boss variant that kicks in when the boss arrives.
  - A sad trombone when you're abandoned, and a fanfare when you evacuate or win.
- **Sound effects**: quiet and distinct per role, with slight random pitch: a tight two-tick rifle burst (three with Extended Mags), a low electric taser buzz, a hollow mortar 'thoonk' and soft foam landing, a sniper crack with a bolt-action click-clack, and a soft rising drone chirp. Also kills, leaks, saboteur clanks, injuries, deploying and reassigning crew, promotions, the boss arrival horn, and UI clicks. The store has a "ka-ching". Effects are panned left or right by their position on the map and rate-limited so big fights don't clip.
- **Settings** (gear button, bottom-right): master, music and effects volume, mute (also the M key), and a screen shake toggle. Settings are saved in the browser. Opening settings mid-contract pauses the game.

## Balance tuning knobs (in index.html)
- `genWave`: wave threat budget `(5.5 + idx*3.3) * (1 + prog*1.7) * diff.mod`
- `spawnEnemy`: HP scaling `(1 + 0.24*idx)` (raised to match perk power)
- `startMission`: starting budget `110 + 10*idx`
- An auto-play bot (greedy placement, no relics, random review picks) won about 75% of simulated runs.

## Next up
Sector 2+, more factions and relics, crew permadeath (an option), real art and audio, a narrative event system, deeper colony meta.
