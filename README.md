# Acceptable Losses

A satirical neo-pixel roguelite tower defence game. You work for **Kindly Security Solutions™**, a private security company that is happy to protect anyone's crystals for the right price and does not care much what happens to you while you do it.

Pick contracts on a star map, deploy a randomly generated crew next to the path, and hold until the drill finishes. If losses push company profit margin to 0%, you're abandoned on a hostile planet.

**Play:** https://kinetrafps.github.io/acceptable-losses/ *(once GitHub Pages is enabled)*

## What's in the vertical slice
- Seven trope worlds (including a cyberpunk Neon Megacity and a Solarpunk Commune), each with themed obstacles, landmarks, weather and planet colour schemes
- Procedurally generated maps with rivers and bridges, lava/acid/water pools, multi-tile buildings that enemies tunnel under and crew can stand on for extra range, and props placed by context
- 5 crew roles, 4 enemy factions in 10 categories (including medics, shields, splitters, stealth and jammers) and 3 tiers, 12 bosses with signature mechanics, and mini-bosses
- Randomly generated crew with quirks who keep their look through the run and can be injured
- Roguelike performance reviews: perk cards each rank, a permanent specialisation at rank 4, capstones at rank 5, and executive perks beyond, with rerolls (appeals) and declines
- Faction envoys who interrupt deployments with pleas and bribes: accept a deal and your crew must let marked enemies through, betray it, or report it to HR. Each faction has a three-beat arc with unique rewards, and HR's emails, the news ticker and the ending follow your choices
- A star map with 4–6 contracts each time, satirical HR emails and payslips, a Company Store that only takes scrip, relics, and a Colony of the Abandoned that gives meta-progression
- Pixel art, music and sound effects all generated in code, with no asset files
- A settings menu for volume, mute and screen shake

## Project layout
- `src/game.html` is the game source, a single self-contained page fragment
- `index.html` is built from it by `node scripts/build.mjs` and served by GitHub Pages
- `DESIGN.md` has the design notes and balance tuning settings

## Controls
Click a crew card (or press 1–8), then a tile next to the path. **Space** starts extraction and pauses. **R** opens a pending performance review. **M** mutes. The gear button opens settings.
