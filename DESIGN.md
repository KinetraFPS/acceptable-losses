# Quarterly Losses: design notes

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
- **Crew** are named towers that carry over between contracts. They gain XP and promotions (a new title, no raise). Saboteurs, ranged hostiles and boss attacks can kill them; a replacement hire inherits their kit.
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
- **Crew gear upgrades** as crew progress:
  - Rank 3: a silver pin and a sight on the weapon.
  - Specialisation: a branch outfit and weapon with its own accent colour for tracers, arcs, shell trails and muzzle flashes:
    - Suppression: helmet and drum-fed LMG. Gunslinger: stetson, gold chain and a gold-plated gun.
    - Storm Caller: violet coil staff. Crowd Control: riot helmet and shock gun.
    - Artillery: beret and long rifled tube. Foam Containment: gas mask and foam cannon.
    - Wetwork: balaclava and suppressed rifle. Spotter: boonie hat and designator rifle.
    - Swarm Manager: glowing visor and tinted drones. Field Medic: white coat with a red cross.
  - Capstone: armour plating, a gold pin, a glowing accent line on the weapon, wider glowing tracers with accent sparks, a steady weapon glow and rising aura motes.
  - Capstone at rank 7+: gold trim, and more aura motes.
- **Death**: crew who are killed stay dead and lie under a sheet with a marker flag. Their card offers **Hire replacement** for `1.5 × fee + 10 × rank` budget:
  - A new person with a different face and name takes over the same role, rank, perks, specialisation and quirk.
  - The Field Medic's revive now fast-tracks a replacement for free after 8s.
  - Anyone still dead when the contract ends is replaced automatically for 15 scrip on the payslip, and HR's email names who died and who replaced them.
  - The final screens list the fallen "In memoriam".
- **Firing**: weapons track the target smoothly and kick back on recoil. Effects include muzzle flash sprites and light, ejected shell casings, gunner two-round bursts, taser arcs, foam mortar shells with smoke trails and foam splats, the marksman's charging laser sight and screen shake, and the drone's hover-and-tilt.
- **Enemies**: humans for the miner, protester and VectorCorp factions use the same random people generator with faction outfits and props. Each faction has its own vehicle (treads, van, walker) and drone. Humans walk on a 4-frame cycle (contact, passing with a lifted foot, other contact, passing) with a swinging back arm, and walker mechs stride with opposing legs, a lifted swing foot and the hull dipping on each footfall. Wildlife are hand-built creature sprites with 4-frame walk cycles, timed to distance travelled so feet don't slide. Four-legged creatures step in diagonal pairs, with far legs drawn darker behind the body, feet lifting on the forward swing, and body, head and tail bobbing. Insects use a tripod gait, and worms, wyrms, the leviathan and slugs send a wave back along the body. Veterans get a white outline and Elites a gold one.
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

## Sectors
A run is three sectors (acts), each of four contracts plus a boss.
- **Sector 1** uses the original seven worlds and ends with a faction boss. Beating it shows a *Sector cleared* promotion notice:
  - The board advances up to 20% margin "against future earnings".
  - Crew, relics and story carry over.
- **Sector 2** (contracts 6–10) adds two new worlds, and at least two of them appear on every Sector 2 map:
  - **Cloud City**: steel deck plating and brass walkways over a gas giant. Rivers and pools of open sky, sky villas, fans, masts, tethered balloons and cargo, a docked airship, drifting clouds. More flyers, faster enemies, +10% crew range.
  - **Precursor Tomb**: dark stone with glowing pink and teal glyphs, psychic pools, ziggurat temples, monoliths, statues, rune pillars and braziers, a giant eye obelisk, whispering motes. Enemies +10% HP and regenerate, crew fire 5% slower.
- Difficulty keeps rising in Sector 2, but each contract counts as about 0.55 of a Sector 1 step, and extraction time grows more slowly.
- The finale is the faction's **apex boss**:
  - **The Union Hall**: the walking union hall seals itself twice behind four Hauler Rigs, rallies and stuns.
  - **The World Serpent**: burrows, spits acid at three crew, regenerates, and splits into three serpentlings.
  - **The Chairman (Gold Exosuit)**: blinks, fires on three crew, EMPs, and comes back flying when "removed".
  - **The Revolution**: a mecha made of thousands of protesters that sheds seven every 10% of health, rallies, heals and gets a second wind.
- **Sector 3** (contracts 11–15) adds the **Kindly Arcology**, and at least two of them appear on every Sector 3 map:
  - Polished concrete plazas and dark walkways with yellow lane markings, glass-curtain office blocks with helipads and revolving doors, reflecting pools, planters, bollards, CCTV posts, info kiosks, statues of the Kindly sun mascot, a branded skyscraper, and memos drifting down between the towers.
  - Company property: enemies +10% HP, crew fire 5% faster with management watching.
- Each Sector 3 contract counts as about 0.32 of a Sector 1 step, and extraction time stops growing after contract 11.
- The Sector 2 boss is now an ordinary faction boss ("Executive priority"). The apex bosses, envoys' reckoning beats and the endings happen at the end of Sector 3 ("Board priority").

## UI feel
- **Transitions:** every screen arrives behind pixel shutters that slide away, and its content rises in one item after another (email paragraphs, payslip rows, store offers, roster, review cards, envoy offer panels). Before each mission the ship flies out to the chosen planet with a warp trail and a flash.
- **Rewards:**
  - Payslip net counts up, then gets a PAID* stamp.
  - Purchases pop with confetti and a SOLD stamp, and the scrip balance ticks.
  - Picking a perk bursts gold confetti.
  - Promotions show a banner and confetti at the crew member.
  - Banners for *Extraction complete* (with confetti), *Deal honoured*, *Sector cleared*, and a hazard-striped *Warning* for boss arrivals.
  - Elite and boss kills float their bounty. The budget readout bumps when it grows, and the margin meter shakes when hit.
- **Polish:** button shine on hover, springy hover on cards and the crew roster, a glowing pulse on crew with reviews due, glints running along meters, bouncing toasts.
- **Star map:** a scan ring and faction · biome line on the hovered planet, a sector banner when you enter a new sector, sector-numbered progress.
- Reduced-motion settings switch the animations off.

## Envoys and deals
Every envoy says their piece in two lines (plus a line about your standing with them): who they are and what they want. The ask, reward and risk panels carry the numbers.
Before some deployments a faction's envoy gets onto your channel. This is what sets the game apart: some deals mean certain enemies must get **through**, and you spend your own margin to keep a promise.

**When envoys appear**
- Not on the first contract.
- Chance on a faction's planet is 20%, plus 12% for every earlier contract against that faction, plus 35% if you're already in that faction's arc. The first sector guarantees one by contract 3.
- Planets with an envoy waiting show *ENCRYPTED CHATTER* on the star map and in the contract card. While an arc is under way, that faction usually has a planet on offer.
- Pleas come from the Union, Wildlife, Activists, Lumen Kin, the Abandoned, the Precursors and the Church. Bribes come from VectorCorp, the Free Haulers, Asset Protection, and from evil clients committing insurance fraud (18% chance when no faction envoy appears).

**The envoy screen**
- An animated pixel video call: the envoy over a faction backdrop. The envoy steps further out of the shadow at each beat.
- **Envoy rigs:** every envoy is a sculpted, lit portrait built from shaded volumes (head, neck, torso, props) rather than flat shapes, so they read as solid forms (`RIGS`, `sculptBall`, `sculptTorso`, `humanHead`).
  - **Idle:** breathing, blinking, and a moving mouth while their lines type out.
  - **Reactions:** accept gets a nod and a smile. Refuse gets a head shake, then they look away while the call dims. Report gets a flash of shock, then anger, then the feed cuts to static and SIGNAL LOST.
  - Character gags stay in proportion (Brent from Claims has a normal neck and tie) so they read as characterisation, not drawing errors.
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

### Reporting to HR
Reporting an envoy pays in relations, never scrip: Kindly's trust in you rises (loyalty +1, which still unlocks the corporate perks), HR suspicion drops by 10, the reported faction's standing falls (−2; −1 for truce and side offers), its closest friend that is around this act falls by 1 and its closest enemy rises by 1. The call screen shows exactly which way each moves before you choose ("If reported: Kindly +1 · Striking Miners −2 · Protesters −1 · Rival Contractors +1").

### Friends, enemies and side deals
Factions have friends and enemies (`ALLY_PAIRS`, `RIVAL_PAIRS`): the union with the activists and the Abandoned, VectorCorp with Asset Protection, the wildlife with the Kin and the Kin with the Precursors, and so on; rivals include the union and VectorCorp, the miners and the wildlife, the Church and the Precursors.

Besides each faction's three-part storyline, a contract can bring a **side deal** (about one contract in five once the storylines are under way), offered by the faction you are fighting, one of its enemies or one of its friends, and shaped by the client:

| Deal | Who calls | When | Reward |
|---|---|---|---|
| Back Pay | the faction you fight | the client is a bad one | standing +1 with them and their friends |
| Quiet Shift | the faction you fight | the client is a decent one | this contract's waves 25% smaller, standing +1 |
| Common Enemy | an enemy of the faction you fight | always | hostiles take 15% more damage this contract; standing +1 with the caller, −1 with your target |
| Safe Passage | a friend of the faction you fight | always (the marked units are your target's own people) | standing +1 with the caller and with your target |
| Salvage Rights | a bribing faction (VectorCorp, the Haulers, Asset Protection) | always | scrip now (30 + 10 per act), standing +1 |
| Lost Paperwork | anyone | HR suspicion 35 or more | HR suspicion −25, standing +1 |
| Paper Trail | the faction you fight | the client is a bad one | standing +1 with them and their friends, Kindly −1 |
| Transfer Request | the faction you fight | you are on good terms and have room | a rank 2 recruit, standing +1 |

Side deals use the usual deal mechanics (let the marked units through; breaking it costs standing) but never change a faction's storyline. Coded as `side:<deal>:<target>` beats so they travel through saves and the existing deal code.

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
| Asset Protected | Completed the Asset Protection arc | Director Haldane |
| The Eternal Quarter | Completed the Church arc | The Deacon |
| Employee of the Quarter | Loyalty 2+ (refused or reported) and honoured no deals | Q. |
| Acceptable Losses | Anything else | Q. |

The final screen also shows the ending number and a **Your Story** recap of every envoy choice. Endings found are saved in the browser and shown on the title screen as "Endings found: n/10".

**Rescues:** if you're abandoned with an arc at beat 2 or later (not betrayed or reported), that faction comes for you:
- Union: Dot's ore hauler.
- Wildlife: the hive carries you underground.
- Activists: Glitch crowdfunds a sponsored shuttle.
- VectorCorp: Mr. Sable "acquires your debt".

- **How the ending is chosen** (`pickEnding`), in order:
  1. Two or more betrayals: Broken Promises.
  2. Defected: Coalition (Hostile Work Environment) if two or more other factions are your allies, otherwise your faction's own ending.
  3. Loyal, every faction purged: Total Market Share (new).
  4. Two finished storylines: Coalition. One: that faction's ending.
  5. Two or more reports to HR: Employee of the Quarter (the informant's Loyalist ending).
  6. No reports and no honoured deals: Clean Hands (new; the bystander who chose nothing).
  7. Otherwise: Acceptable Losses.

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

## Naval and air hostiles
- **Naval** (Ore Barge, Repo Patrol Boat, Protest Flotilla, Snapjaw): appear from contract 3 on maps whose water reaches the edge. They sail the river from the map edge to the water nearest the drill (`computeWaterPath`), shell crew on the banks, then land `unload + tier` troops on the nearest road (`navalUnload`).
- **Gunships** (Survey Copter, Repo Gunship, News Chopper, Sky Ray): fly straight at the drill and strafe crew on the way. Only anti-air crew can hit them.
- Both have 4-frame sprites per faction: spinning rotors, a flapping manta, and bobbing hulls with a wake.

## Artifacts
Bosses drop a crate when they die (mini-bosses 40% of the time). The crate parachutes in and holds an artifact from that boss's faction. If you already own both of that faction's artifacts, it upgrades one instead (up to level 3). You keep artifacts for the whole run.

Artifacts come in two kinds:

- **Platforms** (boats and rays) are the only ones that stay on the map. Each gets a card in the roster bar; place it once per contract and a crew member can stand on it.
- **Abilities** are everything else. Each gets a square on the ability bar at the bottom right of the map, with a hotkey (Q W E A S D Z X C, in order), a cooldown sweep and the seconds left. Every ability is ready when a contract starts, then waits for its cooldown. Aimed abilities wait for a click on the map, with a preview of the area; clicking the square again or pressing Escape cancels. The point is to turn what used to be a steady trickle of value into bursts the player times to save a wave.
- **Loadout.** Only so many abilities go on a contract: 4 slots in acts 1 and 2, 5 in act 3, 6 from act 4 (the helicopter's gunship and airlift share one slot). Before extraction starts, a loadout panel above the ability bar lists every owned ability and toggles which ones go; it disappears, and the loadout locks, when extraction begins. The loadout carries over between contracts. A newly found artifact takes a free slot if there is one; otherwise the drop banner says to swap it in before a contract. An ability taken off the loadout stays off. Without the cap, the bot had about 18 artifacts by act 5 and fired an ability every few seconds.

| Kind | Artifacts | Use | Effect (level 1; per level) | Cooldown |
|---|---|---|---|---|
| Platform | Union Freight Barge, Smuggler's Skiff (water); Tamed Sky Ray, Lantern Kite, Floating Dais (any non-road tile) | Place once | A crew member stands on it for +15–20% range (+5%) | — |
| Barricade | Picket Line Bulldozer, Repurposed Drill Rig, Security Checkpoint | Click a road | A block hostiles must batter through: 1,500 HP (+750), scaled with difficulty, for 10s (+2s). Gone when wrecked | 30s (−2s, min 18) |
| Gunship | Executive Helicopter | Instant | Flies in over the thickest crowd for 6s (+1s): door gun 10 rounds a second at 12 damage (+50%) with 5 splash, and a 60-damage rocket (stuns 0.4s) about every second. Scales with difficulty like the orbital strike. Leaves when done | 45s (−4s, min 28) |
| Airlift | Executive Helicopter | Pick crew, then a tile | Flies in, carries one crew member to any buildable tile, leaves. Not while the gunship is out | 15s (−2s, min 6) |
| Strike | Orbital Billing Satellite, Broadside Battery | Click a point | 320 damage (+50%) in a 1.3-tile circle after 0.8s; bosses take 60% | 25s (−3s, min 10) |
| Jam | Pirate Broadcast Van, Waking Obelisk, Swinging Censer | Click a point | For 8s (+1s), hostiles within 2.5 tiles (+0.3) are slowed 50% (+5%), take 35% more damage (+5%) and lose their cloaks | 26s (−2s, min 16) |
| Spotlight | Livestream Blimp, Surveillance Blimp | Click a point | For 8s (+1s), hostiles within 3.2 tiles (+0.3) take 40% more damage (+5%) and lose their cloaks | 26s (−2s, min 16) |
| Heal | Great Village Lantern, The Break Room, The Confessional | Instant | Every living crew member heals 40% of their health (+10%), then 6 HP/s (+2) for 6s; cloaked hostiles are revealed meanwhile. Does not bring back the dead | 35s (−3s, min 20) |
| Hatch | Brood Nest | Click a point | Eight allied hunters (+2) appear there and chase hostiles. Every bite costs the hunter health (8 + 2 per enemy tier, 16 against a boss), so each lasts four or five bites | 24s (−2s, min 15) |

The helicopter no longer has a pad or a patrol: it exists only during a gunship run or an airlift. The test bot (`sim5`) uses abilities the way a player would: heal when the crew average drops below 55%, and everything else only into a crowd of 12 or more, or a boss, aimed at the densest cluster (barricades go on the road tile just ahead of it).

## Factions
Ten factions. Every one fields its own version of all 17 hostile kinds, with its own sprite and name. Each faction's identity comes from its spawn weights (the kinds it didn't field before come in at a low 0.5) and its own trait.

| Faction | Act | Envoy | Trait |
|---|---|---|---|
| Free Miners' Union | 1 | Old Dot | Numbers and pickets |
| Activists | 1 | Glitch | Crowds, cameras and vans |
| Local Wildlife | 1 | WREN-7 | Swarms, broods and flyers |
| **Lumen Kin** | 1 | Sefa Ninelights | The drill drains their villages, so they get up to 30% faster as extraction runs. Their maps have glass huts and lantern posts whose light fades as the seam drains. |
| VectorCorp | 2 | Mr. Sable | Hardware and lawyers |
| **The Abandoned** | 2 | Marguerite Vance | Ex-Kindly staff. Elites wear +3 salvaged armour and carry the names of crew you lost, in this run and earlier ones (stored across runs). |
| **Free Haulers** | 2 | Bex Ironwake (bribes) | Smugglers: boats and gunships are common, and anything that reaches the drill steals 30% more |
| **Precursors** | 2 | The Archivist | Psychic constructs: veterans and elites slow crew within 1.8 tiles by 20% |
| **Kindly Asset Protection** | 3 | Director Ines Haldane (bribes) | Your own company's enforcers. They have read your file: they take 25% less damage from the crew role you have deployed most this run (a toast names it) |
| **The Church of the Eternal Quarter** | 3 | The Deacon | The burnt-out, organised. Their units gain up to +30% HP as your crew's average morale falls, and staff who quit in Act 3 join the Church |

- **The Lumen Kin** are an alien people, deliberately not a real-world stereotype. They are tall and indigo, lit by crystal veins, with crowns of natural crystal growth, woven glass-thread robes, lanterns, glass shields, kites and long-legged striders.
  - **Arc:** Dimming, Promise, Relighting.
  - **Rewards:** the Kin Lantern relic (crew regenerate), Ilo Threefold (a Lightborn marksman) and the Relighting (on the final contract, the drill pulses light that stuns hostiles and heals crew).
- **The Abandoned arc:** Severance, References, Walkout.
  - **Rewards:** the Exit Package relic (replacement hires cost 40% less), Dee Okafor (a Tenured taser technician) and the Colony Marches (allied ex-employees on the final contract).
- **The Free Haulers arc:** Cargo, Contraband, Free Port. They pay you.
  - **Rewards:** the black market, a free artifact and Guild broadsides on the final contract.
- **The Precursors arc:** Sleepers, Archive, Waking.
  - **Rewards:** the Glyph of Patience relic (+20% XP), the Archive's Memory relic (+20% damage to bosses and elites) and the drill's precursor beam on the final contract.
- **The Asset Protection arc:** Inventory, Requisition, Lockdown. Haldane pays scrip.
  - **Rewards:** Executive Clearance (store 20% cheaper), the Asset Protection Kit (crew +15% HP) and Lockdown (on the final contract, snipers hit the four hostiles nearest the drill every 20s).
- **The Church arc:** Collection, Confession, the Rapture.
  - **Rewards:** the Tithe Plate (contracts pay 20% more), Communion (crew morale never falls below 30) and the Rapture (on the final contract, the choir turns the two hostiles nearest the drill to your side every 22s).
- **Act 3 bosses:** the Head of Security, the Repossessor, the Auditor-General and the Compliance Engine (apex); the High Cantor, the Reliquary, the Penitent Engine and the Quarter Incarnate (apex).
- **The rest of each new faction:** each has 3 bosses plus an apex boss, 2 artifacts, a news channel for the desk, planet scenes, a rescue and an ending.
- **Art plugs in through registries:** units, bosses, envoy portraits and backdrops, obstacles, map dressing and artifact sprites (`FAC_ART`, `BOSS_ART`, `ENVOY_ART`, `ENVOY_SCENES`, `OBST_EXTRA`, `FACTION_MAP`, `ART_EXTRA`).

## Crew conscience
Every hire comes with a **personality archetype**, shown on the hiring card, the stat sheet, the store roster and the ship's personnel files. It sets a **moral lean** (good, neutral or evil), the **value** that decides how your choices move their morale, a **passive**, and the voice of their speech bubbles (`PERSONA`, `giveConscience`, `MORALE_RULES`, `EVIL_RULES`). Morale (0–100) is the thin bar along the bottom of their crew card.

| Archetype | Lean | Value | Passive |
|---|---|---|---|
| The Idealist | Good | Idealist | +10% fire rate while Content or better |
| Bleeding Heart | Good | Sympathiser (one faction) | +20% experience |
| Company Man | Neutral | Company Man | Deploy fee −15% |
| Mercenary | Neutral | Mercenary | +$2 budget per kill |
| The Professional | Neutral | Professional | +10% crit chance; morale swings halved |
| Zealot | Evil | Ruthless | +12% damage |
| Thrill Seeker | Evil | Ruthless | +8% fire rate, +5% crit chance |

| Value | Likes | Dislikes |
|---|---|---|
| Idealist | Deals kept, truces, helped planets, good clients | Betrayals, reports, collateral, working for bad people |
| Company Man | Reports, betrayals, boss kills, clean contracts | Deals, helped planets |
| Mercenary | Bribes, clean contracts, boss kills | Bloodbaths, betrayals (bad for business) |
| Sympathiser (one faction) | Helping that faction (+15 for a kept deal) | Betraying (−25) or reporting (−20) them, killing their boss, fighting them (−0.4 per kill) |
| Professional | Feels the Mercenary's reactions at half strength | |
| Ruthless | Betrayals, bloodbaths, boss kills, bad clients | **Only** good deeds: kept deals (−7), truces (−6), helped planets (−4) and charity jobs for good clients (−6) |

- **Everyone:** loses morale when a colleague dies (grief) or a contract goes badly (25%+ margin lost). Morale drifts back towards 62 by up to 5 points per contract. New hires start at 60–78.
- **Morale no longer changes fees.** Unhappiness stacks penalties instead: each tier down keeps the ones above it (`MOOD_FX`, `moodEffects`, `applyMood`). Evil crew get milder versions. On the ship every mood effect, good or bad, is 1.5× as strong.

| Morale | Tier | Good and neutral crew | Evil crew |
|---|---|---|---|
| 80+ | Inspired | +8% damage and fire rate | Bloodthirsty: +8% damage and fire rate |
| 60–79 | Content | — | — |
| Below 60 | Disgruntled | Dragging Feet: −8% fire rate | Bored: −4% fire rate |
| Below 35 | Miserable | + Sloppy: −10% damage | + Half-hearted: −5% damage |
| Below 15 | About to quit | + Downing Tools: stops firing for 2.5s (3.5s on the ship) every 10–16s | + Sulking: −10% range |

- **Quitting:** anyone below 8 at the end of a contract quits (`crewQuits`). Sympathisers join their faction; everyone else joins the Abandoned.
- **Defectors return:** a third of the way into a later contract against that faction, they come back as a named elite in their own face and outfit, with extra HP and armour. Your crew react ("Is that... Quinn?"), and killing them hits everyone's morale except the Company Men (`spawnDefector`).
- **Corporate rewards:**
  - **Loyalty Dividend:** reports (+$25), betrayals (+$15) and refusals (+$10) bank a dividend that is added to your next contract's budget.
  - **Loyalty perks:** at loyalty 2, Mandatory Fun Budget (+10 morale now, and morale settles higher). At loyalty 4, Retention Bonus (the first quitter each sector is talked round).
- **Speech bubbles:** short lines pop up over crew on real events: kills, deal units passing, betrayals, low HP, a boss arriving, defending the ship, and unprompted grumbling or cheer depending on morale. Each line is written for the speaker's voice, and a stripe in their lean's colour (or their faction's, for a Sympathiser) marks it.
  - **Kill lines** depend on what died and who the speaker is (`killClass`, `killLine`). A kill is a person, a machine (drones, vehicles, the Precursors' constructs), a bug (the hive) or an alien (the Kin).
  - Good crew apologise to people and are relieved it was only a robot. Company Men file it. Mercenaries price it. Professionals report it. Evil crew call aliens xeno scum and bugs vermin.
  - A Sympathiser killing their own faction grieves. Good crew fighting a faction you're Friendly with protest ("We were friends with these people!"). Against a Vendetta faction, good crew mutter "they started it" and evil crew shout "Payback!". They are rate-limited (14s per crew member, 3.5s globally), stack instead of overlapping, and flip below crew standing near the top edge (`barkAs`, `drawBarks`).
- **The desk:** shows crew morale, quits, the dividend, and HR's response to low engagement ("A mandatory fun event (unpaid) has been scheduled"). The desk plant now follows crew morale.

## Faction standing
Each faction sits from −3 (Vendetta) to +3 (Allied), shown as seven pips on contract cards, envoy screens, the desk feed and act transitions (`shiftStanding`).

| What you do | Change |
|---|---|
| Honour a deal | +1 |
| Report the envoy | −2 |
| Betray a deal | −2 |
| Break a deal by accident | −1 |
| Kill their boss | −1 |
| Refuse a truce | −1 |

- **Below zero:** their fighters get tougher, +8% HP per point.
- **At +2:** their waves are 10% smaller per point above 1, and up to 10% of their fighters defect mid-wave and fight for you.
- **At +3:** they send a squad of allies on contracts against other factions.
- **Relationships keep developing after a betrayal:**
  - **Truce:** at Hostile or worse, their envoy can return with a Reparations offer: pay in margin, and standing resets to Neutral and the arc resumes.
  - **Favour:** a Friendly faction can offer one on someone else's contract: a free squad of their fighters.
  - **Openers:** every envoy opens with a line that fits your standing, from "Don't hang up" to "Every village on the seam knows your name".

## The manager
Douglas Pryce, Regional Manager, is Kindly in person and the most recurring face in the game (`showOnboarding`, `showQuarterly`, `managerScene`).
- **Day one:** every run opens with his three-line orientation on your ship's bridge: who he is, the job, and the quarterly review. "Sign the waiver" takes you to the star map.
- **Quarterly reviews:** every 3 contracts, on the way from the store to the star map (before any faction demand), he comes aboard and grades the quarter.
  - **Score** = (average stars − 3) × 0.8 + (crew morale − 55) ÷ 25 − (HR suspicion − 20) ÷ 30 + 0.7 per task done − 0.5 per task failed (`grade`).

| Grade | Score | He… | Effect |
|---|---|---|---|
| S | 2.2+ | claps, confetti | +50 scrip and a choice of two pieces of **Executive Technology** |
| A | 1.2+ | points, grins | +90 scrip, +10% margin |
| B | 0.2+ | sips his coffee | +20 scrip ("a pizza voucher") |
| C | −0.8+ | adjusts his tie | Performance Improvement Plan: −40 scrip, HR suspicion +10 |
| D | −1.8+ | facepalms | −15% margin, crew morale −8 |
| F | below | slams his tablet | **Terminated: the run ends.** On your first review it's a final warning instead (graded D) |

- **Tasks:** each review sets two for the next quarter, all of them what the company actually wants (`MGR_TASKS`): Asset Recovery (leave 2 planets crushed), Pacification Quota (150 kills), Whistleblower Programme (report an envoy), Renegotiation (break a deal), Budget Discipline (return $2,500 of unspent budget), Insurance Event (lose a crew member), Zero Shrinkage (two zero-loss contracts). Completing them helps your grade, pleases Company Men, mercenaries and the Ruthless, and sours idealists and sympathisers.
- **Executive Technology** (relics marked `exec`, never sold in the store): Overclocked Neural Contracts (+35% fire rate, +15% damage), Liability Waiver Field (crew take half damage), Asset Write-Off Satellite (every 12s the toughest non-boss hostile is deleted), Bottomless Expense Account (+$300 budget per contract), Time Theft Protocol (extraction 25% shorter), Creative Accounting AI (margin losses halved).
- **The scene:** the most detailed rig in the game, drawn every frame from sculpted layers (`managerFigure`): a full figure with a suit, company tie, ID badge, lapel pin and rimless glasses. His arms are posed with two-bone joint maths (`armIK`, `sculptCapsule`) through tablet tapping, a coffee sip, pointing, an open-armed welcome, clapping, adjusting his tie, a facepalm and a tablet slam. Each line of dialogue drives his pose and face (`mgrType`, `mgrState`), with a smug raised brow, a corporate grin, glances at the tablet, blinking, a glint travelling across his glasses, coffee steam and a slow weight shift. His tablet chart rises or falls with your quarter.
  - It's set on your own bridge in its current fit-out (`mgrBackdrop`), with a hologram over the bridge table: the company logo on day one, the scorecard bars and grade at a review. Great quarters end in confetti, terminations in a red alarm.

## The money
The payslip lists every deduction on its own line. Under it, **Where the money went** shows what Kindly billed the client (about 34–52× your base fee, more for bad clients), the unspent field budget it reclaims (split into executive spending: yachts, consultants, a rebrand of the word "layoffs"), and your pay as a share of the value delivered, usually around 1–3% (`companyLedger`). The mission HUD notes that unspent budget returns to Kindly. Your pay itself is unchanged.

## The ship
One interior, drawn tile by tile, used twice: as the map when a faction boards, and as the deck you walk between contracts (`SHIP_LAYOUT`, `shipDeck`, `shipRooms`, `shipWalls`). It has no buildings: six rooms (quarters, medbay, reactor, crew lounge, cargo hold, bridge) with bulkhead walls and one door each, grated corridors with guide lights, open deck plating in 2×2 panels, coolant tanks, lockers and pipes, and a chamfered hull with portholes.
- **Fit-out follows company standing:** score = margin − 70 + 15 × loyalty − heat ÷ 4 (`companyScore`, `shipTier`).

| Score | Fit-out | Looks like | Hull guns | Remedy prices |
|---|---|---|---|---|
| 50+ | Executive fit-out | Pale chrome, gold trim, plants, red carpet, warm light | 5, +30% damage | ×0.75 |
| 15+ | Standard issue | Clean grey, blue guide lights | 4 | ×1 |
| −15+ | Cost-cutting | Dim, missing panels with exposed wiring, "temporary" tape | 3, −10% damage | ×1.15 |
| Below | Condemned | Rust, puddles, loose cables, flickering red lights, broken coffee machine | 2, −20% damage, taped-over empty mounts | ×1.3 |

- **Walking the ship:** the **Minimise** button on the star map opens the deck (`showShip`). Walk with the arrow keys or WASD, or click a tile to path there. Crew hang out where their personality takes them (idealists in the medbay, company men on the bridge, mercenaries in the lounge, professionals in cargo, the Ruthless by the reactor, anyone miserable in their bunk), wander, and say how they feel. Click a crew member for their archetype, mood effects and recent morale changes.
- **Stations** (stand on one and press E, or click it):
  - **Navigation console:** back to the star map (so is the ▴ Star map button).
  - **Coffee machine:** 15 scrip, everyone +6 morale. Out of order on a Condemned ship.
  - **Jukebox:** a crew party, 45 scrip, everyone +15 (the Ruthless +20).
  - **Payroll terminal:** hazard pay, 30 scrip, mercenaries +25 and everyone else +8.
  - **Wellness pod:** a one-to-one session, 20 scrip, one crew member +25.
  - **Personnel files**, **reactor** (fit-out and fuel status) and **cargo manifest** (artifacts).
  - Each remedy can be used once per contract (sessions once per crew member); prices follow the fit-out (`REMEDIES`, `useRemedy`).

## Ship defence
A bonus level, not a contract: it doesn't advance the run (`showDemand`, `startSiege`, `finishSiege`).
- **The demand:** when a faction reaches Vendetta (−3), its envoy calls on the way back to the star map (at most once every two contracts) and demands scrip on the usual animated video call: 60 + 40 per raid already fought + 15 per act.
  - **Pay:** standing goes back to Wary, the grudge is dropped and the raid count resets.
  - **Refuse (or can't afford it):** the envoy's feed cuts to static and they board your ship.
- **The map is the ship itself** (`shipMap`, same interior and fit-out as the walk). Three airlocks lead down corridors to the fuel core; crew stand anywhere off the corridors, in the rooms or on open deck.
- **Built-in defences:** hull guns on hardpoints track and shoot anything within 3.2 tiles (damage 10 + 3 per difficulty level, scaled by fit-out); blast doors on the three approaches slow anything squeezing through by 35% (`stepShipDefences`).
- **A test of the crew:** waves are much bigger than a contract at the same point (difficulty ×1.6/1.75/1.85 for raids 1–3, on Routine, Elevated and Elevated contracts (raid 3 used to build on Suicidal, which the difficulty rework made ×1.35, and that put raid 3 at ×2.36; hordes on the ship are 40% smaller, at most 40 strong)). Big boarders (55+ base HP: armoured, shields, carriers, berserkers, gunships) get +45% HP and move 22% slower; bosses move 18% slower, and raid 2's boss also gets +25% HP. Every mood effect is 1.5× as strong, and crew call out as the airlocks blow.
- **The raids:** boarders go for the fuel crystals; leaks drain a fuel meter instead of your margin.
  - **Raid 1:** two airlocks, no boss.
  - **Raid 2:** two airlocks and one of the faction's bosses.
  - **Raid 3:** all three airlocks and the faction's apex boss at full force.
  - **Win:** a salvage bounty (+70/+100/+130 scrip), and the next demand comes later.
  - **Lose:** Kindly buys replacement fuel out of your margin (−12%; at 0% you're abandoned), and the raid comes again.
  - **One raid at a time:** after any demand, no faction calls for three contracts.
- **Dissolution:** win raid 3 and the faction is gone for good:
  - It's off the contract pool and act bosses, and its storyline ends.
  - Its worlds read as crushed, and its defectors are gone.
  - Sympathetic crew take it hard (−30 morale), idealists a little (−8), and company men are pleased (+8).
  - Connected factions shift: e.g. dissolving the Union warms the Abandoned and cools the Activists; dissolving Asset Protection warms the Church and the Abandoned.
  - The victory screen lists every faction dissolved on your watch.

## Architecture
Buildings are drawn as solid forms seen at three-quarters, from a **type** (what the building is for) in a **biome's materials** (`B3`: `BT`, `BKIT`).
- **Reading as 3D:**
  - Roofs have a lit and a shaded slope, a ridge and overhanging eaves. The roof styles are gable, hip, flat with parapet, barrel, sawtooth, pressurised dome, green turf and stepped ziggurat.
  - Front walls are tall, with recessed windows, lit sills, stepped doors and a darker side return.
  - Rooftop clutter (chimneys, tanks, AC, dishes, panels) casts its own shadow.
  - Every building has a dark outline and throws a shadow onto the ground to the lower right, longer for taller buildings.
- **Human types:** housing, shop (striped awning), school (flagpole and clock tower, or a rooftop court in cities), clinic (rooftop cross), church (bell tower and rose window; a domed church with a minaret on desert, moon and sky worlds; a megachurch screen in the megacity; an eye temple on tomb worlds), depot (roller doors) and office. City worlds (megacity, Kindly HQ) add **skyscrapers**: setback crowns, a beacon, floor after floor of windows and a long shadow.
- **Fungal types** keep the same building shapes as everywhere else, with the fungus as the material: walls of pale grown mycelium brick, roofs of overlapping shelf-fungus plates, round windows glowing from inside, puffball chimneys breathing spores. Spore homes, a market hall under a gill-striped awning, a **creche** with egg-pods glowing in its windows (in place of a school), a **mender** with a healing pool set into its roof (in place of a hospital), a spore temple with a puffball tower and a glowing gill-disc window, a glass-roofed grow-house and a tall elder hall with shelf fungus at every floor. The precursor tomb uses stone ziggurats and also swaps school and clinic for creche and mender.
- **Materials per biome:**
  - Ice: red polar-station roofs under snow.
  - Desert: adobe with flat roofs and a domed church.
  - Moon: panelled pods under glass domes.
  - Megacity: concrete and neon.
  - Solarpunk: timber, turf roofs and solar panels.
  - Volcanic: basalt and iron, with smoking chimneys.
  - Cloud City: white villas with lavender roofs and brass.
  - Tomb: carved stone ziggurats.
  - Kindly HQ: glass and company yellow.
- **Cities** (megacity, Kindly HQ) get more plots, plots back from the road like city blocks, and mostly towers. Every tower is built level by level, one tile row each, with a terrace on top of every level that crew can stand on (`towerLevels`). Five shapes: setback (a narrow crown and a ledge round it), slab (a helipad, sky gardens on every level, an ad screen), round (a balcony ring on every level), needle (steps in level by level to a lit spire nobody can stand on) and tiered (each level a little wider than the one above; glowing pagoda eaves in the megacity). Housing there is a block of capsule flats with portholes, balconies, laundry, a fire escape and a vertical neon sign.
- **Where crew can stand:** each type has a roof deck. Every tower level has a terrace (not the needle's spire), churches not on the bell tower. The needle and the glass grow-house have no rooftop spot. The front-wall row stays a ground-level cover spot. Tiles a tall landmark (the billboard) overhangs are blocked too.
- **Faction buildings:** on a faction's map, one or two plots become theirs:
  - Union: a Union Hall with banners.
  - Activists: a tagged squat.
  - Wildlife: infested blocks (an ordinary local building with hive growths on the roof, resin down the walls and egg-sacs glowing in the windows).
  - VectorCorp: a branch office.
  - The Abandoned: boarded-up Kindly prefabs.
  - Free Haulers: a guild warehouse.
  - Precursors: a ziggurat with a watching eye.
  - Asset Protection: barracks with a searchlight.
  - The Church: a crimson chapel.
- **Town planning** (`placeBuildings`, `assignTypes`): roads are routed first, and buildings go up along them.
  - The first few line a straight stretch of road as a planned street of matching houses, shops or towers, doors onto the road.
  - Every other plot is scored for nature: a road in front of the door is best, one alongside is fine, the back of a building facing the road is penalised, and plots near other buildings score higher.
  - The biggest free plot becomes the civic landmark.
  - Buildings never sit on a road, always keep a clear tile between them, and never put a door onto water, a wall, another building, a prop or a landmark. A short paved walk runs from each door.
  - Tested over 400 generated maps: no building on a road, none touching, no blocked door, and about three-quarters open straight onto a road.
- **Animations** (`drawBuildingAnim`): waving flags, chimney smoke and steam, flickering neon, office windows switching on and off, blinking beacons, a cycling megachurch screen, pulsing egg-pods, a ripple on the mender pool, spores drifting off caps, light running up the shrine's veins, a glint across Kin glass, the ziggurat's eye looking around, a sweeping searchlight and candles.
- Street lamps stand at even intervals along every road, and the drill sits on a paved plaza.

## Sprite lighting
- **Crew and enemy sprites** get a lighting pass (`sculptHuman`): each row of a figure is lit like a cylinder from the upper left (the same light as the buildings and envoy portraits), keeping its colour on the lit side, with a highlight on the head, shade under each shape, a falloff towards the feet and a cool rim on the shadow edge. It covers crew on the map, card portraits and full-body pictures, and every enemy unit, vehicle, creature and boss.

## Acts
Each sector is an act, with its own cast and its own light (`ACTS`).

| Act | Name | Factions | Look |
|---|---|---|---|
| 1 (Sector 1) | Onboarding: local grievances | Union, Activists, Wildlife, Lumen Kin | Bright daylight |
| 2 (Sector 2) | Restructuring: competition and fallout | VectorCorp, the Abandoned, Free Haulers, Precursors | Dusk and smog: warm skies over purple shadow, drifting smog, rusting abandoned Kindly rigs on the map and in scenes, a red nebula on the star map, a flickering lamp on the desk |
| 3 (Sector 3) | The Endless Quarter: reckoning | Kindly Asset Protection, the Church of the Eternal Quarter | Corporate night: cold blue-black light, company yellow windows and alarm red, a blue banner on the star map |
| 4 (Sector 4) | The Uprising (defected) or Homogenisation (loyal) | Everyone still standing | War light: red-orange over deep crimson |
| 5 (Sector 5) | Overthrow (defected) or Total Market Share (loyal) | Everyone still standing; the final contract is at headquarters | Gold over violet |

- **Unlocking:** a faction first appears when its act arrives. VectorCorp no longer shows up in Act 1.
- **Weighting:** the act's own factions get weight 3. Factions from earlier acts start at 0.3 and gain weight from your history with them: +1.4 for an unfinished envoy arc, +1 for a grudge, +0.6 for a finished arc, and a little per planet you helped or crushed. A fresh Act 2 is about 80% VectorCorp; a run with unfinished business sees old factions much more (`factionWeights`).
- **Bosses:** an act's boss comes from the faction you fought most in that act (`actBossFaction`).
- **Showing it:** contract cards mark factions as "New this act" or give a reason they're back ("Unfinished business", "They remember you", "Old friends", "Back for more"). The sector-cleared screen introduces the next act's cast. The star map opens with an "Act 2: Restructuring" banner.
- **Palette:** `actGrade` lays a soft-light gradient, a multiply tint, a light haze and slow smog bands over the mission, the star map and planet scenes. Planet scenes also swap to the act's sky. Each planet remembers the act it was played in, so the montages show the run's change of light.

## Sides and the endgame
A run is five acts of five contracts (`MAX_SECTOR = 5`); difficulty growth flattens after contract 15 (`diffLevel`).
- **Storyline finales** now come before the boss contract of each of acts 1–3, not only the run's last, so a run can finish more than one storyline (`rollEnvoy`).
- **The invitation:** finish a faction's storyline and, after that act's boss, its envoy invites you to their colony on their own channel (`showInvitation`). The screen shows exactly who would come with you and who would stay. Decline, and they never ask again.
- **Who follows you** (`wouldFollow`): crew at 60+ morale. Sympathisers of that faction always follow; others need 70. Company Men need 85, and crew whose lean opposes the faction's morals (good crew to an evil faction or the reverse) need 82.
- **Defecting** (`defect`):
  - Followers gain 10 morale.
  - The rest go back to Kindly and are added to its defectors, so they turn up against you as named elites.
  - Two of the faction's people join as troops.
  - Your standing with the faction goes to Allied, and Asset Protection's to Vendetta.
  - Douglas Pryce revokes your badge.
- **Faction troops** (`comrade`, `FACTION_KIT`): crew in the faction's colours with an archetype that fits its morals and a kit that improves with rank:
  - Union: Picket Training, damage plus a stun from rank 3.
  - Wildlife: Hive Bond, slowing hits.
  - VectorCorp: Black-Market Optics, range and crit.
  - Activists: Crowdfunded Kit, fire rate and experience.
  - Lumen Kin: Lamp-Blessed, HP and range.
  - Abandoned: Old Kindly Training, cheaper and faster.
  - Free Haulers: Smuggler's Cut, money per kill.
  - Precursors: Archive Sight, damage and crit.
  - Asset Protection: armour.
  - The Church: Choir-Backed.
  - After defecting, the store only hires the faction's troops.
- **Working for them** (`employer`, `sideClient`, `causeMorale`):
  - Your faction is the client on every contract.
  - Enemies are mostly Kindly's Asset Protection, plus anyone not on good terms with your side; allies are never targets.
  - The store becomes their Commissary and the desk their Commons, and unspent budget goes to the common fund (strike funds, clinics, lamp oil).
  - Morale follows the cause: crew whose lean matches the faction's morals gain 4 per contract, opposed crew lose 5, and a neutral cause pleases mercenaries.
  - Pryce's quarterly reviews stop.
- **Faction morals** (`FACTION_MORAL`): good for the Union, the Wildlife, the Lumen Kin, the Abandoned and the Activists. Neutral for the Free Haulers and the Precursors. Evil for VectorCorp, Asset Protection and the Church.
- **Between acts** (`showCrossroads`):

| Moment | Defected | Loyal |
|---|---|---|
| Entering Act 4 | Your faction's council: "Kindly is coming for us. Time we went for them first." | Pryce promotes you to Director of Market Homogenisation |
| Entering Act 5 | Pryce calls, furious: the board is coming for you in person | Pryce: "A few holdouts left. Finish them." |
| Act 4–5 contracts | Mostly against Asset Protection and Kindly loyalists | Beating a faction **purges** it for good: one win if it is Hostile or worse or you have crushed one of its worlds (or it's a boss), two otherwise; contract cards say which (`purgeAfter`) |
| Final contract | The Board: Kindly's board out of the sub-basement with Pryce at the controls (Asset Protection's apex, +35% HP) | The last faction standing's apex, +20% HP |

## Planet scenes and the desk
- **Planet scenes:** each of the 9 worlds has a pixel-art postcard for each of the 4 factions, in 3 states: unresolved (the faction is on site and the drill is contested), helped (you honoured their deal, so the site is theirs and the rig is repainted) and crushed (Kindly flags, guards and the faction's wreckage). That is 108 scenes, built in code from each biome's own sky, ground, road, liquid, building, landmark, props and weather, plus the faction's real unit sprites (`planetScene`, `SCENE_FAC`).
- **The fallen:** resolved scenes show the bodies of the faction's units you killed there, two for every ten kills, up to 12. People and creatures lie on their side in a pool of blood (green ichor for wildlife); machines are dark, smoking wrecks (`sceneFallen`).
- **Continuity:** every finished contract is stored in `RUN.worlds` with its outcome. Contract cards show the planet live and unresolved. A faction you've fought before shows a thumbnail of how you left their last planet. Sector reviews, game over and endings show a montage of your planets.
- **The desk:** the debrief is now a first-person view of your desk.
  - **Kindly Intranet (left):** a one-line HR quip, a performance rating, margin and net pay, a compact payslip, one line per story event, and Kindly News.
  - **Faction channel (right):** Local 404 Radio, VectorCorp Markets, Glitch.Live or the WREN-7 Wildlife Cam. It shows the planet as you left it, with a headline and the strip of your planets.
  - **The desk itself:** a mug, a sticky note, a nameplate, and a plant that wilts as the margin falls.
- **Less reading:** HR letters became one-liners. Endings keep two paragraphs (the setup and the punchline). Termination, sector review and envoy deal terms are each down to a sentence or two.

## Line of sight, cover and targeting
- **Crew against buildings:** every building has a strip of pavement along the foot of its front wall (`footing`, 3px, door steps left showing). Where a crew member stands is worked out once per tile (`perchAt`): on the front row they stand on that pavement and throw a shadow onto the wall; at the front edge of a roof their feet sit on the edge and the roof's lip is redrawn over their boots, cut to their outline so it never adds stray pixels, with the gun drawn last so it is held out over the ledge. On towers each level's standable deck is its terrace strip, so crew stand on the terrace with its lit edge across their boots; on open ground in cover they lean 2-3px into the wall beside them, shaded if the wall is between them and the light (upper left), otherwise throwing their shadow onto it.
- **Riding platforms:** the barge, skiff, sky ray, lantern kite and floating dais are drawn in layers around their rider (`RIDE`, `rideSprite`, `drawRide`): the platform, then the crew member standing on its deck row and moving with its bob or rocking, then the platform's front layer (gunwale, basket, near lip) over their boots. The rider is sorted with the platform as one item.
- **Frame errors:** the frame loop survives an exception, resets the canvas state so a half-finished draw cannot leave the screen tinted, and the toast names the functions involved. Colour helpers treat a missing colour as grey instead of throwing. Enemy gunfire colours (`SHOT_COL`) cover every faction.
- **Line of sight:** buildings block what crew on the ground can see. Crew on rooftops or the sky ray see over them, drones fly over them, and mortars lob over them. Flyers are always visible. Hostiles can only shoot crew who can see them. When you place or select crew, blind spots inside the range ring are shaded and red-hatched (`sightMap`, `canSee`).
- **Cover:** props near buildings now sit on the corners, so the walls are free. Crew on a tile next to a building wall are in cover and take 20% less damage. So are crew on a building's bottom row: that is its front wall, so they stand in front of it at street level, with no rooftop range bonus and ground-level line of sight. The placement ghost shows a shield on cover tiles (`coverAt`, `facadeAt`, `COVER_DR`).
- **Preferred targets:** every crew member has a targeting mode: First, Last, Strongest, Weakest, Closest, Flyers (anti-air crew only) or Elites. It is set from the info panel, and kept for the rest of the run (`PRIO`, `crew.prio`). Marksmen default to Strongest; everyone else defaults to First.
- **Crew bar:** cards are bigger, and show role and status. Hovering or focusing a card extends it upward into a stat sheet: DPS, range, HP, what the crew member hits, what they're good against, their targeting mode, quirk and perks. On touch screens, the selected card keeps its sheet open.
- **Helicopter patrol:** once its pad is down, the Executive Helicopter flies after whichever hostile its own targeting mode prefers, and the door gunner fires at anything close. With nothing on the map, it circles the pad. Clicking its card starts an airlift straight away when it is ready, and opens its orders panel (targeting chips and airlift status) alongside. Click the card again to cancel.
- **Conditions:** crew no longer stand on a wooden pallet, just a soft shadow. What is true of them right now is listed as text on the info panel (which refreshes live) and the crew card stat sheet: holding position, Golden Handcuffs, stunned or offline, jammed, badly hurt, rooftop, barge or sky ray deck, in cover, being healed, boosted, protected, and a waiting review (`crewConditions`).
- **Battle damage:** hostiles and bosses degrade as they lose health. Below 75% they show scorch marks and a crack, below 50% more of both, and below 25% chunks are blown out with glowing rims; badly hurt units also trail smoke and sparks. The marks are seeded per sprite, so they stay put across animation frames (`damagedFrame`).

## Crew progression: performance reviews
Each promotion gives a small base boost (+10% damage, +3% fire rate, +12 HP per rank) and a **performance review** in which you pick a card. Reviews can be held mid-contract (click the highlighted crew card, or press R; the game pauses) or between contracts ("Hold performance reviews").

| Rank | Review | Options |
|---|---|---|
| 2 | Tier I · Common | 3 cards: role perks topped up with corporate perks |
| 3 | Tier II · Rare | 3 cards: mechanic changers (armour shred, multishot, cluster shells, executes, extra drones...) |
| 4 | Specialisation | 1 of 2 permanent branches per role, each showing its future capstone |
| 5 | Capstone | the branch capstone, or one of 2 Tier II cards |
| 6–12 | Executive | high-impact perks with trade-offs (Golden Handcuffs, Burnout Protocol, Stock Options, Tenure Track, Unpaid Overtime, Pension Raid, Keynote Speaker...) |

- **Branches**: Turret Operator (Suppression Specialist / Hazard Pay Gunslinger), Taser Tech (Storm Caller / Crowd Control Officer), Mortar (Long-Range Artillery / Foam Containment), Marksman (Wetwork Contractor / Spotter), Drone Operator (Drone Swarm Manager / Field Medic).
- **Capstones** include map-wide lightning, freezing pulses, 5-shell barrages, damage-amplifying foam, executes that refund the reload, spreading marks, 4-drone hive minds, and a protective medic aura.
- **Quirks**: every hire rolls one of 10 traits (Nepotism Hire, Tenured, Office Gossip...). They're shown in the store before you hire.
- **Appeal decision** rerolls the cards for scrip (10, then +5 each time). **Decline promotion** takes 12 scrip instead.
- **Synergies**: marks (Tracer Rounds, Static Cling, Spotter, Quagmire foam) amplify all crew damage. Auras buff, heal or protect crew within 1.5 tiles.
- **Level cap 12** (`MAXL`). XP thresholds: 16 / 45 / 95 / 165 / 265 / 395 / 560 / 770 / 1030 / 1340 / 1700. Levels 9–12 add +25 max HP each instead of +12 (264 HP at level 12). Ranks 9–12: Associate Director, Director of Associates, Chief Associate Officer, Associate for Life.
- **Levels follow the acts** (see *The difficulty model*): a promotion freeze caps crew at level 4 / 6 / 8 / 10 / 12 in acts 1–5, so the last levels land in the final act.

## Crew types
| Type | Fee | Plays as | Specialisations (capstone) |
|---|---|---|---|
| Turret Operator | 40 | Reliable single-target fire, air and ground | Suppression Specialist (Pinned Down) / Hazard Pay Gunslinger (Deadeye) |
| **Arc Technician** (reworked taser) | 50 | Chain lightning: jumps through up to 3 hostiles (each jump at 80% of the last), slowing each | Storm Caller (Act of God) / Crowd Control Officer (Total Lockdown) |
| Foam Mortar Crew | 70 | Lobbed splash, ground only | Long-Range Artillery (barrage) / Foam Containment (quagmire) |
| Marksman (Intern) | 80 | Long range, ignores armour, targets the toughest | Wetwork Contractor / Spotter |
| Drone Operator | 60 | Rapid fire, triple damage to flyers | Drone Swarm Manager / Field Medic |
| **Thermal Compliance Officer** (new) | 55 | Flamethrower: burns everything in a cone, every second burst leaves fire on the ground. Ground only | Scorched Earth: fire every burst, +40% burning (Controlled Burn: a firestorm every 8s) / Pressure Cooker: +35% range, strips armour (Meltdown: strips all of it) |
| **Railgun Auditor** (new) | 90 | A slug through every hostile in a line, armour-piercing, hits air | Forensic Auditor: everything hit takes +25% damage (Write-Down: a kill recharges the gun in 0.45s) / Capacitor Overclock: +40% damage, +20% range (Gauss Volley: every 3rd shot fires twice) |
| **HR Liaison** (new) | 40 | Doesn't fight. Crew in its 2.4-tile range fire 20% faster and hit 15% harder; hostiles there are 20% slower | Culture Champion: a stronger aura (Mandatory Offsite: aura heals and protects) / Policy Enforcer: hostiles 30% slower and take +15% damage (Performance Improvement Plan: they lose armour too) |

- **The taser rework:** it used to pulse weakly at everything around it. The Arc Technician throws lightning at a target and it chains on to the nearest hostiles; its perks now read as chains (Arc Jump adds jumps, Overcharge and Total Lockdown count discharges).
- **Balance check** (three crew of one type, a whole contract): Marksman, Railgun and Mortar lose least, Drone and Turret sit in the middle, and the flamethrower and Arc Technician were buffed to close the gap. The Liaison pays off in a fuller roster, where its aura covers several crew.

## Water, fire and burning

- **Water** (`buildWaterFrames`): every liquid gets a looping ripple layer, baked into 16 frames when the mission starts and played at 9 fps. Three travelling waves summed per pixel give lit crests, a fainter ripple band, shaded troughs and the odd glint. The water darkens with its true distance from the shore (a chamfer pass over the map), and foam laps along the edge in a slow surge. Lava gets molten crests and a cooling crust, the sky biome only soft white crests, the ship's coolant a 1px band.
- **Fire on the ground** (`fireFrames`, `drawFireZone`): scorched ground, a bed of mostly dark coals with live embers, and rows of flame tongues rising across the patch, back to front, swaying and breaking up at the tips. Baked once per patch size into 12 frames; patches start at different frames so they never flicker in step. Embers and smoke rise off them, and they light the ground around them.
- **Burning hostiles**: anything caught by a flamer cone or standing in fire burns for about a second after (`burnT`): a scorched tint, and flames licking up from the sprite's own outline (`burnFrames`, six frames per sprite frame), with smoke and an orange glow. Visual only: burning does no extra damage.
- **Burnt to the bone**: a humanoid that dies on fire writhes and blackens, the char flakes away to ash and the skeleton shows through, then the skeleton gives way. The legs buckle first, everything above drops onto them, and the skull lands last and rolls. The bones lie on a scorch mark for a few seconds before fading. At most ten burn at once; the rest die the ordinary way.

## Kill effects
How a human hostile dies depends on what killed it (`killK`, set in `damage` from the crew member's class, or from `DMG_SRC`, which explosion code sets around its damage loop). Bosses, flyers and anything in a tunnel keep the plain burst.

| Killed by | Kind | What you see |
|---|---|---|
| Flamer, or anything while the target is burning | burn | Writhes in flames, chars, flakes to ash, and the skeleton collapses (above) |
| Arc Technician | shock | A cartoon electrocution. The victim snaps into a shocked pose drawn by `drawHuman` itself ('zap' arms flung up, 'zap2' arms flung out; legs splayed, hair on end, eyes white, mouth open, hat and prop knocked away). For 0.85s it is lifted and buzzing, flicking at 22Hz between that pose outlined in white and its x-ray: the pose's own silhouette in deep blue with a pale outline, and a white skeleton laid out bone for bone in the same pixel grid (`zapBones`: skull with sockets and jaw, collarbone, spine, ribs and pelvis sized to the build, arm bones along the flung sleeves, leg bones down the splayed legs), cut to the body's outline. Bolts crawl off it, the light strobes white and cyan, a low buzz plays (`zapdie`). Then it stops in the pose, charred grey-black, hair smoking, white eyes blinking twice, and falls to grey dust from the head down, leaving a grey ash pile. The Kin, who are not drawn by `drawHuman`, are x-rayed in their walking frame with a generic skeleton cut to their outline |
| Every gun, the gunship's door gun, allied bites | shot | An articulated fall (`FALL_KEYS`): the frame is cut into legs, torso and head, pivoting on the feet, hips and neck, each lagging the one below. The hit snaps the chest and head back and sprays blood away from the shooter; the body staggers, the head whips forward, the knees go, it slumps on its knees with the head lolling, tips over away from the shooter, hits the ground with a thud and a dust puff, the chest and head bounce, and it settles with the head to one side. Two small twitches later, while a pool spreads out from under it |
| Foam shells, gunship rockets, orbital strikes and broadsides | blast | Comes apart: head, torso and both legs are cut from the frame (each with a raw edge), thrown away from the blast, spin, bounce and settle flat with a splat where each lands; a scorch where they stood |

Blood is the faction's (`BLOOD`): red for people, blue for the Kin, pink for the Precursors. Each kind has a cap on how many play at once (shock 14, shot 24, blast 14; burn 10); past it, a kill falls back to the plain burst, so a horde wiped by one shell stays cheap. Gib pieces are cut once per variant frame and kept.

**Creatures and ground machines.** The same weapon kinds, played their own way (`d.fam`). Creatures are every `creature` variant except the Precursors' stone constructs; ground machines are `vehicle` variants that neither fly nor float (treads, vans, walkers). Only bosses (and lieutenants) still use the plain burst; flyers, boats and the Precursor constructs have their own (below).

| | Creatures (wildlife, Kin striders) | Ground machines (treads, vans, walkers) |
|---|---|---|
| Gun | Knocked back, rolls onto its back with a hop and a thud, legs kicking (walk frames swapping, slowing), then still in a spreading pool of its faction's ichor | Shudders and sparks, pops (a small blast and sound) at 0.35s, then a dark, slumped wreck with fire burning out on it, an oil slick and smoke |
| Taser | The cartoon x-ray, with a skeleton fitted to the creature's own outline (`fishBones`: a spine down the middle of the body, a rib every third column), then charred and crumbling to grey dust | EMP: glitches in horizontal bands and flashes white with arcs crawling over it, pops at 0.7s, then the wreck, still throwing blue sparks |
| Explosion | Bursts into three slices, front to back, each with an ichor edge; splats where they land | A fireball, and the wreck breaks into four pieces of scorched metal that bounce, settle and smoke |
| Fire | Writhes in flames and blackens, curls up (squashes towards the ground), then falls to grey ash | Flames pour off it while it blackens, then the wreck burns out |

Wrecks (`wreckFrames`: the frame darkened and scorched) and ash frames are built in the per-frame warm-up (`warmVariant`), so the first death of a kind does not stall a frame. Burning creatures and wrecks add a fading orange light.

**Flyers, boats and stone.**

| | Flyers (drones, gunships, flying creatures) | Boats | Precursor constructs (stone) |
|---|---|---|---|
| Gun | Spins out of the sky trailing smoke, drifting away from the shooter (`airFall`: 10px up, 0.55s down). Gunships blow apart where they hit (a fireball and four pieces of wreck); drones crash with sparks and lie wrecked, burning out; creatures splat and lie on their backs in ichor | Lists away from the shooter and sinks below the waterline, bubbling, with a ripple; the water line closes over it | Cracks spread from the middle of the body (`crackPixels`), lit pink with white tips and a pink glow, then it shatters into six chunks with glowing pink breaks, which bounce and settle (`crumble` sound) |
| Taser | Stalls in the air for 0.4s, flashing white with arcs, then drops straight down | Arcs crawl over the hull and it flashes white, then it sinks | Overcharges, flickering white and pink while the cracks spread, then shatters |
| Explosion | Blown apart in the air; the pieces fall and bounce | Splits in two; the halves tip apart and both sink, with a splash | Shatters outward at once |
| Fire | Falls trailing flame, and burns out on the ground | Burns at the waterline, blackening, then sinks | Heats red-hot, then crumbles from the top into a rubble pile |

## Protest props
Crowds mix their props (`crowdProp`): most carry a placard in one of six styles (scrawled board, cardboard, NO, coloured board, heart, two-pole banner), the rest torches, flares, drums or megaphones; union pickets add pickaxes and pitchforks, activist hardliners torches, molotovs and bats, the Abandoned cardboard and pitchforks, the Church banners and torches. Torches, flares and molotovs carry a flickering light (`propLights`).

## Rendering performance
Profiled on a busy Act 3 map (eight crew, 90–150 hostiles, 60–95 lights): about 30 fps before this pass, about 53 fps after, with the slowest 5% of frames down from 51–57 ms to 26–28 ms (a browser with no graphics card; real GPUs have more headroom).
- **Grades on the pixel buffer.** The world's colour grade (soft-light) and the act's light (soft-light, multiply, haze, smog bands) used to be full-screen blends at screen resolution every frame. They now run on the 396×234 pixel buffer before it's scaled up: the same look over about 1/30th of the pixels.
- **A baked vignette.** One cached image per screen size instead of a new radial gradient every frame.
- **Light sprites.** Each light colour gets one soft radial sprite, scaled per light, instead of a new gradient for every light every frame. Lights carried by hostiles are capped at 60 a frame.
- **One-draw outlines.** Rank outlines (veteran, elite), slow and deal markings and the selected crew member's outline were four offset copies of a silhouette; they're baked into one outline image (`ring4`).
- **A quieter HUD.** The budget's bump animation (which forces a layout), the crew cards' affordability check and the speed buttons no longer run on every kill or every frame.
- Earlier passes: battle-damage, burn and fire frames are baked and built at most three per frame; water is a baked loop.

## Stutter
Diagnosed with a per-frame timing harness (frame time, simulation steps, simulation and render time, and which functions ran in each slow frame) on a busy Act 3 map at 1x, 2x and 3x.
- **The cause:** the first time a new kind of hostile appeared, its whole pool of looks (ten for people) was built in one simulation step: sprites, shading and 16 coloured silhouettes each, 20–35 ms in one frame. Since the difficulty rework brings new kinds and hordes all contract long, it happened again and again. At 3x every hitch was followed by catch-up frames of 6–12 simulation steps, so hostiles visibly jumped.
- **Built at load** (`prewarmPools`): every look the faction can field this act, its demoted bosses from Act 3, about 0.4 s when the contract loads. Hit-flash silhouettes and, from Act 2, rank outlines are warmed in the background two looks a frame (`warmVariant`).
- **Lazy silhouettes** (`lazySilhouettes`): the hit-flash, rank and slow silhouettes are built when first needed, under the same three-a-frame allowance as battle damage and burn flames (`silReady`); a sprite drawn before its silhouette is ready just skips the outline for a frame.
- **One new look a frame** for anything not built at load (`getVariant`, `POOL_TARGET`).
- **Catch-up is capped** at the game speed plus two steps a frame; past that the game falls a moment behind rather than jumping.
- **The flamethrower**, not the railgun, was the costliest of the new classes: every enemy it lit built its burn flames at once, and each fire patch shed embers every drawn frame. Burn flames now share the per-frame allowance, patches shed embers and smoke on game time (particle ceiling 260), and glowing particles no longer build a colour string each.
- Result: the worst simulation frame fell from 43–59 ms to 11–13 ms at every speed, and slow frames in a 14 s capture from 32 to 5. Railgun, flamethrower and Arc Technician squads now cost about the same as the classic crew.

## Spawn grace
Hostiles can't be shot or damaged for their first 0.1 seconds (`SPAWN_GRACE`): crew don't target them and no hit, splash, zone or chain lands, so every arrival reads on screen before it can pop. It applies to every spawn, including bosses, lieutenants, splitter children and troops a ship unloads.

## Saving and resuming
- A run saves itself (browser storage, key `al_run`) at the points it can be picked up cleanly: the star map, the store (every purchase and reroll), using a remedy on the ship, the start of each contract and raid, and a faction's invitation.
- The title screen offers **Resume shift** with the sector, contract, margin and crew count; **Clock in (new run)** replaces the save.
- A contract or raid that was under way when the game closed **starts again from the top**, so reloading can't dodge a bad contract or lose a won one. Quitting after a win lands you in the store with the rewards kept.
- Losing or winning deletes the save. The save is plain JSON (about 17–20 KB); contracts are re-pointed at the faction and world tables on load, and a save that can't be read is discarded with a note on the title screen.

## Audio
- Everything is synthesised live with Web Audio. There are no audio files. Audio starts on the first tap or key press, which is a browser rule.
- **Music**: a small chiptune sequencer.
  - Corporate hold music on the menus, mail and store; drifting arpeggios on the star map.
  - **One mission song, arranged per world** (`BIOME_MUSIC`): the melody, chords and bass stay the mission theme's, and each world swaps instruments, tempo, drums and a texture.

    | World | Arrangement |
    |---|---|
    | Frozen | **Its own song**: cold and spacious, D minor at 100 bpm, a triangle melody in the middle register over a soft pad with echo, a soft kick, snow crunch instead of hats, quiet sine arpeggios an octave up |
    | Toxic | Wobbly triangle lead, triangle arpeggios |
    | Dust | Twangy plucked lead, shaker, a loping kick |
    | Low gravity (Crystal Moon) | **Its own song**: floating and glassy but round, E minor like the main theme (Em, Cmaj7, Am7, B) at 92 bpm, a triangle melody in the middle register on chord tones, a soft half-time kick with no snare or hats, a warm pad, a light echo, quiet triangle arpeggios. Replaced an arrangement whose sine lead up around B4 to B5 sounded like whistling (spectral centroid 1,550 Hz; now 420 Hz, against 580 Hz for the ice song) |
    | Cyber | Filtered square lead, constant triangle arpeggios an octave lower, busy hats |
    | Solar | Triangle lead, bells and shaker |
    | Volcanic | **Its own song**: E harmonic minor (Em, C, Am, B) at 112 bpm, a low round triangle melody over a warm chord pad, a pumping triangle bass with sub-bass on the downbeats, forge toms, a dull anvil on 2 and 4, a lava rumble |
    | Cloud | Airy triangle lead, pad, echo |
    | Tomb | A semitone down, choir pad, sparse kick, no hats |
    | HQ | Corporate chord stabs and steady hats |
    | Ship | Four-on-the-floor with dull metallic knocks |

  - **No whistling.** A pure tone high up (a sine above about 700 Hz, a triangle above about 950 Hz) reads as whistling, so nothing plays there. `whistle.js` lists every sine or triangle voice per track that would reach that range, and the renders are scored by the share of energy in narrow tonal peaks between 850 Hz and 2.6 kHz. The scan found and fixed:
    - the evil-contract ghost: a sine a tritone above every melody note on every track (930 to 1,400 Hz) is now a triangle a tritone below;
    - the bell (Solar Commune, Lumen, Abandoned): a sine an octave above the melody (up to 2,350 Hz) now chimes in unison with it;
    - the Lumen theme: a sine melody around F#5 to D6 is now a triangle an octave down (whistle share 9.5% to 0.2%);
    - the jungle, desert, solar and cloud arrangements: the mission melody on a triangle reaching B5 now plays an octave down (`leadOct`);
    - the main menu and the manager's hold music: a square melody up to C6 and arpeggios two octaves up, both down an octave (menu 8.1% to 2.2%; what is left is the square's buzz, not a whistle);
    - the choir (Church, Precursors, tomb): two octaves over the chords, now one.
    Every track now scores 2.2% or less.

    It still adds layers as the drill fills. Arrangements avoid bright square and saw leads up high and keep the middle of the mix full: the old forge arrangement had the weakest middle of the set (4.5% of its energy between 250 Hz and 1.5 kHz, against 10.8% for the old frozen one), and it sounded thin and tinny over a muddy low end. The old frozen arrangement had the opposite problem: the brightest top of the set, from a bell sparkle two octaves above the lead, high arpeggios and hats, so it got its own song too and the bell sparkle everywhere dropped an octave.
  - **Faction themes** (`FACTION_THEMES`) play on each faction's calls, demands and invitations, over the envoy's slow pad:
    - Union: a work-song in G, with hammer clanks.
    - Activists: a protest chant in A minor with a backbeat.
    - Wildlife: tribal toms and insect clicks under a wobbling lead.
    - Lumen Kin: a slow sine hymn in D with bells.
    - VectorCorp: a cold saw arpeggio in C minor on four-on-the-floor.
    - The Abandoned: a music-box waltz in A minor.
    - The Haulers: a twangy shuffle in E.
    - The Archive: a sparse harmonic-minor choir.
    - Asset Protection: a C-minor march with a snare roll.
    - The Church: an organ hymn in F.
    - The manager gets the hold music, a semitone flat and in no hurry.
  - **The boss layer**: the music no longer switches track when a boss arrives. A boss layer comes in over the world's own song instead (half as much for a mini-boss): double-time kick, snare fills, a pumping triangle octave bass, soft filtered chord stabs, constant arpeggios, a brighter filter and up to +7% tempo. It eases in over a couple of bars and back out after the kill.
  - **The uncanny layer**: on an immoral contract the same song turns slightly wrong:
    - everything drifts a few cents off true;
    - the chord's fifth sags to a tritone on alternate bars;
    - the arpeggio now and then lands a semitone wide;
    - the lead wobbles, with a faint ghost of every note a tritone up;
    - the hats thin out.

    A contract counts as immoral when you work for "Bad people", or, after defecting, when your side is VectorCorp, Asset Protection or the Church.
  - A sad trombone when you're abandoned, and a fanfare when you evacuate or win.
  - **Staying in key**: every melody keeps to one key (the minor-key songs use one seventh degree, not both), strong beats sit on chord tones, vibrato is set in cents so a low note wobbles no wider than a high one (default 9 cents, toxic 16, wildlife 18), and the twang slides up into each note from 0.6% under it instead of sagging flat. The uncanny layer is the only thing meant to sound off.
- **On the beat**: the sequencer keeps a beat clock (`beatNow`). Crew bop on it, half on the beat and half off; flower heads sway with it; the crystal deposit pulses with it, harder on the downbeat.
- **Sound effects**: quiet and distinct per role, with slight random pitch: a tight two-tick rifle burst (three with Extended Mags), a low electric taser buzz, a hollow mortar 'thoonk' and soft foam landing, a sniper crack with a bolt-action click-clack, and a soft rising drone chirp. Also kills, leaks, saboteur clanks, injuries, deploying and reassigning crew, promotions, the boss arrival horn, and UI clicks. The store has a "ka-ching". Effects are panned left or right by their position on the map and rate-limited so big fights don't clip.
- **Ambience** (kept to what reads and costs next to nothing):
  - **Wind gusts** about every 14s in the windy worlds (frozen, dust, solar, cloud, toxic, HQ, tomb): a few streaks, the weather pushed sideways, flowers leaning.
  - **Birds** that suit the world, a few at a time: songbirds (solar), gulls (frozen, cloud), vultures circling (dust), bats (tomb), pigeons (HQ), moths (toxic). Big blasts flush them.
  - Not animated, on purpose: enemies stay off the beat so their movement reads as threat, and trees and buildings don't sway (they're baked sprites, and redrawing them every frame would cost the frame rate). No birds where there's no air or open sky (low gravity, the forge, the cyber city, the ship).
  - A stress test with 160–190 hostiles showed no frame-rate difference.
- **Settings** (gear button, bottom-right): master, music and effects volume, mute (also the M key), and a screen shake toggle. Settings are saved in the browser. Opening settings mid-contract pauses the game.

## The difficulty model
Difficulty is designed from a planned crew-power curve rather than tuned run by run. In the old curve the best crew member hit level 12 by contract 6, the rank mix stopped changing after Act 2, Acts 2–4 cost almost no margin and Act 5 then wiped crews.

- **Crew pace.** XP is steady pay: every deployed crew member gets the contract's completion XP (`COMPLETION_XP` 14 / 24 / 40 / 66 / 125 by act), the bench half, and anyone three or more ranks below the sector's ceiling double. Kills add a little on top (`killXp`, about 30% of bounty early, falling as waves grow). A **promotion freeze** caps levels per act (`ACT_CAP` 4 / 6 / 8 / 10 / 12); XP over the cap is banked and the reviews fall due when the next sector starts. Crew cards say when a promotion is frozen.
- **Planned power.** Roster size (3 rising to 8) × level gains (+10% damage, +3% fire rate per level) × the perk each review adds (Tier I ×1.13, Tier II ×1.2, specialisation ×1.3, capstone ×1.25, executive ×1.12) × a small allowance for relics.
- **Wave threat** (`threatAt`) is anchored at the end of each act and interpolated geometrically: 0.85 at contract 0, then 4.6 / 15.9 / 37.9 / 87.4 / 156. The anchors come from that planned power against the old curve: Act 1 holds its old pressure, Acts 2–4 rise by 25–35% (they had gone slack) and Act 5 eases 5%. Threat splits into more hostiles (`waveBudget` = 5 × threat^0.55) and tougher ones (`waveHp` = threat^0.45).
- **Every vector steps up per act** (`ACT_STEP`):

  | Act | Armour (not swarms) | Speed | Veterans | Elites | Elite traits | Lanes |
  |---|---|---|---|---|---|---|
  | 1 | +0 | ×1 | 5% | 0% | 30% from contract 2 | 1–2 |
  | 2 | +0 | ×1.03 | 20% | 6% | one each | 2 |
  | 3 | +1 | ×1.06 | 32% | 13% | one; veterans 20% | 2 |
  | 4 | +2 | ×1.09 | 42% | 20% | half carry two; veterans 35% | 3 |
  | 5 | +3 | ×1.12 | 50% | 28% | two each; veterans 50% | 3 |

  These are what each act builds up to by its boss: every value blends from the previous act's across the act's contracts (`actStep`), so no single contract takes every step at once. Rank shares also rise as the drill fills.
- **Unlocks** (`UNLOCK_ACT`): the basics from the start; Medics and Splitters in Act 1; Shields, Stealth, Ranged, Berserkers, Gunships and naval craft in Act 2; Jammers, Carriers, Blinkers and Burrowers in Act 3. Each comes in lightly in its first act.
- **Hordes** (`genHorde`): every 5th wave in Act 1, every 4th in acts 2–3 and every 3rd in acts 4–5 (one sooner on Suicidal). A horde is one kind of grunt (Swarm, Runners, or Flyers from Act 2), 12–60 strong, packed close and spread over every lane, announced on arrival. Ordinary waves stay mixed, so a contract reads as mixed, mixed, horde, with the bosses on top.
- **The boss ladder.** Act 1: one mini-boss a contract and the act boss. Act 2: two mini-bosses. Act 3: the faction's bosses also walk in with ordinary waves as **lieutenants** (shrunken boss sprites, gold-outlined, the boss's armour and auras, about an elite's toughness). Act 4: lieutenants in ordinary waves, and every other horde is a pack of 4–6 of them. Act 5: every horde is 6–9 lieutenants, and one mini-boss each contract is the faction's apex.
- **Boss HP by act** (`BOSS_ACT`): ×0.45 / 0.65 / 0.9 / 1.5 / 1.8 of the faction's listed HP, from the same power curve (no level-10 carry in Act 1 any more; a full level-12 crew in Act 5). Mini-bosses follow the wave HP curve (`0.9 × waveHp`); apex understudies at 12% of the apex.
- **Stun resistance.** Bosses take 40% of a stun, mini-bosses and lieutenants 60%, elites 80%. Every stun adds resistance (+25% for bosses and lieutenants, +10% for others, up to 80%) that fades at 12% a second, and a boss can't be stunned for 1.5s after one ends (0.8s for minis and lieutenants). A thin bar under the health bar shows it: blue while resistance builds, grey while immune. Bosses and lieutenants also take half the slow.
- **Suicidal** contracts mean it: ×1.35 threat (HP through its square root), +1 lane, ranks one step up (+15% veterans, +10% elites), traits ×1.5, hordes one wave sooner, a third mini-boss, more lieutenants. They pay ×1.6, plus hazard pay (25 + 15 per act) and a requisitioned rare or very rare relic.
- **Upgrade power budget.** Tier I: about +12–15% to one stat (Gym Membership +50% HP → +30%). Tier II: about +20–30% or utility (Hostile Takeover +40% → +30%). Capstones define the build. Executive: +20–30% to one thing, or a trade (Golden Handcuffs +30%/+30% → +20%/+20%, Burnout +60%/−40% → +40%/−30%, Tenure +40%/+15% → +30%/+10%).
- **Relics** come in three tiers: common (about 60 scrip; Scopes, Loyalty Card, Insurance, Overtime, Signing Bonus, Interns, Ammo), rare from Act 2 (about 110; Poster, Coffee Machine, Golden Parachute) and very rare from Act 3 (about 170; Liability Waiver, now +40% HP, and Overclocked Tasers). Prices rise 15% each act.
- Unchanged: the wave interval (13s, tightening with `diffLevel` and drill progress), the starting budget, and enemy gun damage and heal auras on `lateIdx`.


**Tuning after the ability rework.** Bot runs (15 full runs each) showed act 1 killing most runs, mostly through Suicidal contracts taken before the first artifact drops, and acts 3 to 5 becoming trivial once the bot used abilities. So:

- Suicidal contracts in act 1 use ×1.2 instead of ×1.35 (same pay).
- Waves in acts 3, 4 and 5 carry 10%, 12% and 15% more (`ACT_THREAT`, applied in `waveThreat` before the budget and health split; budget × health is linear in threat, so these are straight percentages of hostile health per wave). Lieutenant and boss thresholds still read the raw `threatAt`.
- Abilities are capped by the loadout (above).
## Next up
Sector 2+, more factions and relics, crew permadeath (an option), real art and audio, a narrative event system, deeper colony meta.
