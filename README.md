# Acceptable Losses

A satirical neo-pixel roguelite tower defence game. You work for **Kindly Security Solutions™**, a private security company that is happy to protect anyone's crystals for the right price and does not care much what happens to you while you do it.

Pick contracts on a star map, deploy a randomly generated crew next to the path, and hold until the drill finishes. If losses push company profit margin to 0%, you're abandoned on a hostile planet.

**Play:** https://kinetrafps.github.io/acceptable-losses/ *(once GitHub Pages is enabled)*

## What's in the vertical slice
- Three sectors with ten trope worlds (including a cyberpunk Neon Megacity, a Solarpunk Commune, a Cloud City, a Precursor Tomb and Kindly's own corporate arcology) and apex bosses in the finale, each with themed obstacles, landmarks, weather and planet colour schemes
- Procedurally generated maps with rivers and bridges, lava/acid/water pools, multi-tile buildings that enemies tunnel under and crew can stand on for extra range, and props placed by context
- 5 crew roles, 10 enemy factions in 17 categories (medics, shields, splitters, stealth, jammers, plus ranged shooters, reinforcement carriers, teleporters, berserkers and burrowers) and 3 tiers, elite traits, 28 bosses with signature mechanics, mini-bosses, and difficulty that keeps climbing through the run
- Naval and air hostiles: boats sail up rivers, shell the banks and land troops near the drill; gunships fly straight in and strafe crew
- Faction artifacts dropped by bosses and fielded beside the crew: a freight barge that makes water buildable, a bulldozer that blocks the road, an executive helicopter that chases targets by targeting mode and airlifts crew, an orbital billing strike, a broadcast van, a livestream blimp, a tamed sky ray platform and a brood nest of allied hunters
- Line of sight: buildings hide hostiles from crew on the ground (blind spots are shaded), rooftops see over them, and crew against a wall are in cover. Each crew member has a targeting mode (first, last, strongest, weakest, closest, flyers, elites)
- A crew bar whose cards extend into a stat sheet on hover (DPS, range, HP, quirk, perks), and hostiles that visibly break apart as they take damage
- A pixel-art postcard of every world and faction in three states (contested, theirs, the company's) that follows your choices through the run: on contract cards, on a first-person desk debrief with Kindly's intranet beside the faction's own news channel, and in montages at the end of each sector and run
- Three acts with their own cast and light: daylight, then Act 2's dusk and smog, then Act 3's corporate night, across the map, star map, planet scenes and desk, while older factions come back based on your history with them
- Ten factions across three acts, each fielding its own version of all 17 hostile kinds: Lumen Kin villages lit by the crystal seam, ex-Kindly staff carrying the names of your fallen crew, smugglers, waking Precursor constructs, Kindly's own Asset Protection (who study your most-used crew role) and the Church of the Eternal Quarter (who grow stronger as your crew despair)
- Faction standing from Vendetta to Allied: truces after betrayals, favours between friends, defectors and allied squads
- Bespoke architecture for every world in planned rows, with plazas, yards and street lamps
- Crew personalities: seven archetypes with a good, neutral or evil lean and a passive, shown when you hire. They react to your choices and your clients; unhappy crew stack penalties up to downing tools, evil crew only sour on good deeds, quitters defect and come back wearing your kit, and speech bubbles fit the speaker and what they just killed
- Your ship: minimise the star map to walk its decks, talk to the crew and spend scrip on coffee, parties, hazard pay and counselling. Its fit-out, from Executive to Condemned, follows your standing with the company
- Store rerolls for scrip
- Randomly generated crew with quirks who keep their look through the run and can be injured
- Roguelike performance reviews: perk cards each rank, a permanent specialisation at rank 4, capstones at rank 5, and executive perks beyond, with rerolls (appeals) and declines
- Faction envoys on animated video calls, as sculpted, lit pixel portraits that blink, talk and react to your answer (a nod, a turned head, a cut signal), who interrupt deployments with pleas and bribes: accept a deal and your crew must let marked enemies through, betray it, or report it to HR. Each faction has a three-beat arc with unique rewards, and HR's emails, the news ticker, ten endings and even who rescues you when you're abandoned follow your choices
- A star map with 4–6 contracts each time, satirical HR emails and payslips, a Company Store that only takes scrip, relics, and a Colony of the Abandoned that gives meta-progression
- Pixel art, music and sound effects all generated in code, with no asset files
- A settings menu for volume, mute and screen shake

## Project layout
- `src/game.html` is the game source, a single self-contained page fragment
- `index.html` is built from it by `node scripts/build.mjs` and served by GitHub Pages
- `DESIGN.md` has the design notes and balance tuning settings

## Controls
Click a crew card (or press 1–8), then a tile next to the path. **Space** starts extraction and pauses. **R** opens a pending performance review. **M** mutes. The gear button opens settings.
