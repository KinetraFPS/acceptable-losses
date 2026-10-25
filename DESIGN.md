# Acceptable Losses: design notes

Satirical roguelite tower defence. You work for Kindly Security Solutions™, an immoral private
security company. You defend clients' crystal extractions across Earth and the galaxy.

## Core loop (vertical slice)
1. **Star map**: pick one of 4–6 contracts (planet bubbles) with random difficulty and faction. Each shows the client, whether they're good or bad people, the hostile faction, biome hazard, difficulty and pay. Planets flagged **ENCRYPTED CHATTER** have an envoy waiting.
1. **Envoy call** (sometimes): a faction's envoy makes a plea or offers a bribe before you land. See *Envoys and deals*.
2. **Mission** (about 2.5–4.5 min): procedurally generated map. Deploy crew next to the path and hold until the drill reaches 100%, then clear the area to evacuate.
3. **Debrief**: a satirical HR email plus a payslip in Company Scrip, with itemised deductions.
4. **Company Store**: hire crew, buy relics, promote crew, or use creative accounting to restore margin.
5. Repeat. Sector 1 is 4 contracts, then a boss. The boss faction is whichever faction you fought most.

## Rules
- **Profit margin** is run-wide HP (starts at 100%). Leaked enemies reduce it. At 0% you're abandoned and stranded.
- **Budget** is spent during a mission to deploy crew (from kills plus a trickle). **Scrip** is spent between missions, only at the store.
- **Crew** are named towers that carry over between contracts. They gain XP and promotions (a new title, no raise). Saboteurs can injure them for the rest of a contract.
- **Enemies**: 15 categories × 3 tiers (Grunt, Veteran, Elite), skinned per faction. The five core types (Swarm, Runner, Armoured, Flyer, Saboteur) are joined from contract 2 by five specials, and from contract 3 by five nastier behaviours. Each is introduced with a toast the first time it appears in a run:
  - **Medic** heals nearby hostiles. **Shield** cuts damage to nearby hostiles by 30%. **Splitter** bursts into smaller hostiles. **Stealth** cloaks on and off; crew only see it up close or once it's marked. **Jammer** makes nearby crew fire 35% slower.
  - Union: First Aider, Strike Committee, Union Rep. Protesters: Umbrella Bloc, Group Chat Admin, Livestream Crew. VectorCorp: Wellness Officer, Riot Contractor, Cloaked Counsel. Wildlife: Spore Nurse, Brood Sac, Chameleon Stalker.
  - Contract 3 onwards, three of these five per faction:
    - **Ranged** shoots crew from 2.6 tiles while walking, slowing down to aim.
    - **Carrier** calls in two reinforcements every 6s.
    - **Blinker** teleports 2.2 tiles along the path every 5s.
    - **Berserker** gets up to 90% faster and 30% tougher as it's hurt.
    - **Burrower** goes underground and out of reach for 2s in every 6.
  - New types per faction:
    - Union: Rivet Slinger, Union Recruiter, Tunnel Rat.
    - Wildlife: Acid Spitter, Burrow Wyrm, Frenzied Ravager.
    - VectorCorp: Hostile Auditor, Fixer, Middle Manager.
    - Protesters: Egg Thrower, Influencer, Flash Mobber.
- **Elite traits**: from contract 3, some elites (15%, rising 15% per contract) and later veterans arrive with a trait, shown by a coloured pip over their head:
  - **Swift**: +30% speed.
  - **Hardened**: +4 armour.
  - **Regenerating**: heals 2% HP per second.
  - **Volatile**: explodes on death, hurting nearby crew.
- **Bosses**: five per faction, one picked for each sector finale:
  - Union: Shop Steward Mk.IV (summons picketers), General Strike (bulldozer that periodically rallies every hostile +45% speed), Collective Bargaining Unit (van that slows crew within 2.5 tiles by 50%), **The Pension Fund** (armoured vault that seals itself at 66% and 33% health until three Hauler Rig guards die), **Former Employee of the Month** (defected Kindly mech that charges and slams the ground, hurting and stunning nearby crew).
  - Protesters: The Influencer (summons followers), The Movement (CEO effigy giving 50% damage reduction nearby), #Trending (blimp that goes viral and floods every entrance), **Critical Mass** (a crowd boss that sheds six protesters every 12% of health lost and rallies the map), **Hunger Striker** (mobile sit-in: guilt slows nearby crew 45%, heals nearby hostiles, second wind at 20% back to 60%).
  - VectorCorp: Regional Manager (flies, drops spies), Acquisitions Division (EMP knocks nearby crew offline for 2.5s), C-Suite Executive (when killed, deploys a Golden Parachute and returns flying at half health), **Chief Legal Officer** (files injunctions at 66% and 33%: untouchable under a golden dome until three Riot Contractors fall; slows nearby crew), **Severance Package** (termination robot that fires on three crew every 5s and sprints).
  - Wildlife: Brood Matriarch (regenerates, lays gasbags), Sand Leviathan (burrows untouchable, surfaces with a swarm), Mother of Spores (heals everything within 3 tiles), **The Hive Mind** (flying brain that blinks three tiles closer every 8s and lays gasbags), **Thornback Colossus** (spits acid at two crew every 6s; two calves burst out when it dies).
- **Mini-bosses**: from contract 3, an "Understudy" version of a faction boss (30% HP) turns up at 65% extraction. It takes its cut once instead of circling back.
- **Persistence**: factions you've fought return with a grudge (+10% HP). The boss is chosen from your history. Hints about the mind-control twist show up in email P.S. lines.
- **Meta**: every failed run adds a survivor to the Colony of the Abandoned (+5 starting scrip each, capped at 50).

## Art direction: neo-pixel
- The playfield is drawn into a low-res buffer (1 art px = 2 game px) and scaled up crisply. Lights, tracers, taser arcs, muzzle flashes and the laser sight are drawn on top at full resolution with additive glow.
- **Crew** are 12×17 chibi sprites. The body is random (10 skin tones, 12 hair styles including afro, braids, bun and headscarf, natural or dyed hair colours, facial hair, glasses, build, and extras like freckles, an eyepatch or a plaster). The role sets the outfit: hi-vis guard, taser tech with a battery pack, hard-hat mortar crew, pink-polo intern with a lanyard, hoodie drone operator. Everyone stands on a company-issued pallet.
- **Firing**: weapons track the target smoothly and kick back on recoil. Effects include muzzle flash sprites and light, ejected shell casings, gunner two-round bursts, taser arcs, foam mortar shells with smoke trails and foam splats, the marksman's charging laser sight and screen shake, and the drone's hover-and-tilt.
- **Enemies**: humans for the miner, protester and VectorCorp factions use the same random people generator with faction outfits and props. Each faction has its own vehicle (treads, van, walker) and drone. Wildlife are hand-built creature sprites with 4-frame walk cycles, timed to distance travelled so feet don't slide. Four-legged creatures step in diagonal pairs, with far legs drawn darker behind the body, feet lifting on the forward swing, and body, head and tail bobbing. Insects use a tripod gait, and worms, wyrms, the leviathan and slugs send a wave back along the body. Veterans get a white outline and Elites a gold one.
- **Terrain**: per-biome noise ground, a path sunk below the ground, biome decorations, and obstacle sprites with their own light sources.
- **Spawn points** are animated transit chambers on steel landing pads:
  - The sliding doors open just before a hostile arrives, flooding the path with blue light.
  - A transporter beam materialises the hostile: first blue scanlines, then the real sprite fading in. It can't be targeted for those 0.45s.
  - The doors close once it has walked out.
- **The client's crystals** are a cluster of 12 faceted crystals (light, mid and dark faces, tips, edge highlights, travelling glints) on an ore mound under the drill rig:
  - The number visible follows your profit margin.
  - When margin is lost, the smallest crystals break off first, shattering into shards and leaving stumps. The big central crystal goes last.

## Map generation
Maps are built in this order, so the big structures shape the roads rather than being sprinkled on afterwards:
1. **Drill site and spawns**: the drill sits on the right; spawns are on the left, top or bottom edges, well apart.
2. **River** (most worlds, about 50–70% of maps): a one-tile river runs edge to edge. Roads cross it on **bridges** (wooden, or metal on industrial worlds).
3. **Buildings**: 2–4 multi-tile buildings (2×2 up to 4×2 / 2×4), clear of the drill and each other. Crew can stand on the roof and get **+15% range** (high ground).
4. **Roads**: Dijkstra over tile *and heading*, so every turn costs extra and roads come out as long straight runs instead of staircases. Roads are drawn towards buildings, so most maps send at least one road **through a building as a tunnel**. Enemies inside a tunnel are hidden and can't be targeted or damaged until they come out. Crew can still stand on the roof above.
5. **Validation**: a map is rejected and rebuilt if it has a 2×2 block of road, a road brushing against itself, or two roads running side by side for more than two tiles. This stops the clustered, stair-stepping roads.
6. **Pools**: blobs of the world's liquid on open ground.
7. **Props by context**: each world sorts its props into rules, and every prop only goes where its rule allows:
   - road: signs, kiosks, drills
   - building: vents, dumpsters, vaporators
   - shore: reeds, ice, obsidian
   - grove: small clusters of trees, crystals or mushrooms away from the road
   - open: a few lone rocks

Liquids can't be built on, and each world has its own:

| World | Liquid |
|---|---|
| Ice World | Freezing water with ice floes |
| Death World Jungle | Bubbling acid |
| Desert Planet | Oasis with reeds (pools only) |
| Crystal Moon | Liquid methane (pools only) |
| Neon Megacity | Canal with neon reflections |
| Solarpunk Commune | Pond with lily pads |
| Forge World | Lava with crust and glow |

Liquids shimmer, and acid, methane and lava bubble. Buildings are styled per world: neon apartment blocks, terracotta eco-houses with solar roofs and gardens, snow-dusted station modules, whitewashed desert domes, moon habitats, moss-covered bunkers, and hazard-striped foundries with smoking chimneys.

## Envoys and deals
Before some deployments a faction's envoy gets onto your channel. This is what sets the game apart: some deals mean certain enemies must get **through**, and you spend your own margin to keep a promise.

**When envoys appear**
- Not on the first contract.
- Chance on a faction's planet is 20%, plus 12% for every earlier contract against that faction, plus 35% if you're already in that faction's arc. The first sector guarantees one by contract 3.
- Planets with an envoy waiting show *ENCRYPTED CHATTER* on the star map and in the contract card. While an arc is under way, that faction usually has a planet on offer.
- Pleas come from the Union, Wildlife and Activists. Bribes come from VectorCorp, and from evil clients committing insurance fraud (18% chance when no faction envoy appears).

**The envoy screen**
- An animated pixel video call: the envoy's bust over a faction backdrop. The envoy steps further out of the shadow at each beat.
- The envoy's message types out using details from your run: the planet, the client, last time's results, injured crew.
- An offer panel lists the ask, the reward and the risk.
- Choices: **Accept**, **Refuse**, or **Report to HR**. Reporting pays scrip and loyalty, but that faction holds a grudge (+15% HP) and never calls again. Two refusals and the envoy stops asking.

**Deals in the field**
- Accepting spawns **marked units** during the drill. They have a green outline and a white pennant.
- Crew automatically hold fire on marked units, including chains, arcs, thunder and barrages. Mortar splash, napalm and foam can still kill them.
- A dead marked unit **breaks the deal**. The HUD has a **Betray** button to break it on purpose.
- Breaking a deal: the faction turns hostile (+20% HP), you lose the reward, and bribes are clawed back.
- Marked units that reach the drill cost the agreed margin.

**Heat**
- Each accepted deal raises Heat (HR suspicion), shown on the star map.
- Heat cools by 5 per contract. At 75, an internal audit takes 25 scrip and cuts Heat by 30.

**The paper trail**
- HR-BOT's debrief email reacts to every honoured, broken, refused or reported deal, plus your Heat level.
- Honoured deals add headlines to the news ticker.
- The victory screen and game over screen change with your choices (see *Endings*).

**Deal types**
- **Couriers**: marked units reach the drill and leave with crystals (margin).
- **Skim**: marked drones siphon the drill (margin).
- **Escort**: brood sacs nest at the drill. No crystals, but each one extends the extraction.
- **Uplink**: hackers stand at the drill uploading. The drill pauses while they work.

| Faction | Envoy | Type | Beat 1: Contact | Beat 2: Trust | Beat 3: Reckoning (before the final contract) |
|---|---|---|---|---|---|
| Miners' Union | **Old Dot**, union recording secretary, in a lantern-lit mine shaft | Plea · couriers | *Strike Fund*: 4 × 3%. **Picket Line** relic (crew next to crew +10% fire rate) | *The Walkout*: 5 × 3%. **Rafa Okonkwo** joins (rank 3 mortar, *Unionised*: +20% dmg) | *General Strike*: 6 × 2%. Every 22s three allied miners march out from the drill, stunning and hitting hostiles |
| VectorCorp | **Mr. Sable**, SVP of Opportunities, in a neon penthouse | Bribe · skim | *Quiet Acquisition*: 3 × 4%. +60 scrip up front | *Due Diligence*: 4 × 4%. +40 scrip and a **Black Market** in the store (Black Card, Document Shredder, Poison Pill) | *Hostile Takeover*: 5 × 4%. The final boss arrives with −30% HP and permanently marked |
| Wildlife | **WREN-7**, an abandoned survey drone adopted by the hive, in glowing hive tunnels | Plea · escort | *Migration*: 3 sacs × 8s. **Pheromone Tag** relic (wildlife 25% slower) | *The Nursery*: 4 × 8s. **Biscuit**, a pet Lopehound that patrols a path biting hostiles and gets back up 15s after being knocked out | *The Swarm Hunts*: 5 × 6s. Every 15s six allied skitterlings burst from the drill and hunt the boss |
| Activists | **Glitch**, masked streamer and hacker, in a graffiti alley | Plea · uplink | *The Leak*: 1 hacker × 10s. **Leaked Schedule** relic (cloaked hostiles always visible, plus a readout of each wave) | *Doxxed*: 2 × 10s. **Doxxed** relic (elites and bosses take +15% damage) | *Livestream*: 3 × 8s. The final boss is "cancelled" for 25s: abilities off, +25% damage taken |
| Evil clients | **Brent from Claims**, in a boardroom | Bribe · couriers (the contract's own hostiles) | *Act of God*, one-off, up to twice a run: 4 × 4%. +50 scrip now, half the margin refunded when the "claim" pays. Heat +30 | | |

The reckoning envoy appears before the final contract, whichever faction the final target belongs to.

## Endings
The victory email changes with the run. Endings are checked in this order:

| Ending | Condition | Sender |
|---|---|---|
| Broken Promises | Broke 2+ deals, by betrayal or accident | Q., delighted |
| Hostile Work Environment | Completed 2+ faction arcs | Everyone you helped |
| Solidarity | Completed the Union arc | Dot |
| The New Board | Completed the VectorCorp arc | VectorCorp Board |
| Apex Predator | Completed the Wildlife arc | WREN-7 (translated) |
| Going Viral | Completed the Activists arc | Glitch, live |
| Employee of the Quarter | Loyalty 2+ (refused or reported) and honoured no deals | Q. |
| Acceptable Losses | Anything else | Q. |

The final screen also shows the ending number and a **Your Story** recap of every envoy choice. Endings found are saved in the browser and shown on the title screen as "Endings found: n/8".

**Rescues:** if you're abandoned with an arc at beat 2 or later (not betrayed or reported), that faction comes for you:
- Union: Dot's ore hauler.
- Wildlife: the hive carries you underground.
- Activists: Glitch crowdfunds a sponsored shuttle.
- VectorCorp: Mr. Sable "acquires your debt".

## Worlds
Seven trope worlds, each with its own ground and path palette, path treatment, ground decor, props sorted by context, a liquid, its own building style, a 2x2 landmark (0–1 per map), animated props, weather, a colour grade, and 2–3 planet colour schemes on the star map.

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
Difficulty is tuned to rise through the run rather than flatten out as your crew levels up.
- `genWave`: wave threat budget `(5.5 + idx*3.0 + idx²*0.3) * (1 + prog*1.8) * diff.mod`
- `genWave`: veteran rate `-0.04 + idx*0.14 + prog*0.3` (max 68%), elite rate `-0.2 + idx*0.08 + prog*0.16` (max 34%)
- Wave interval: 13s, tightening from contract 4 by 0.9s per contract and up to 2.4s as the drill fills (minimum 8.5s)
- `spawnEnemy`: HP scaling `(1 + 0.22*idx + 0.03*idx²)`
- Bosses have +10% HP. Understudies have `30% × (1 + 0.2*idx)`.
- `startMission`: starting budget `110 + 10*idx`
- The auto-play bot (greedy placement, random contracts, random review picks) wins about 28% of runs, down from 67% before this pass (80 runs each). Average margin lost per contract:
  - Before: 11 / 21 / 26 / 15 / 5% (it got easier as crew levelled).
  - Now: 12 / 18 / 33 / 25 / 24%.

## Next up
Sector 2+, more factions and relics, crew permadeath (an option), real art and audio, a narrative event system, deeper colony meta.
