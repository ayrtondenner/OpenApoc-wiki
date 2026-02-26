# Development Roadmap

OpenApoc development is tracked through a series of milestone issues on GitHub. The project progresses through three main phases: **Alpha** (playable core mechanics), **Beta** (feature-complete), and **Release 1.0** (polished and fully equivalent to the original game). A fourth tracking issue covers modding, quality-of-life enhancements, and extra features that are handled separately from the main milestones.

This document summarizes the current state of each milestone based on the GitHub issue tracker.

---

## Current State

OpenApoc is currently in **Alpha**. Most core game mechanics are implemented, and the game is playable from start to finish, though some features remain incomplete or have known issues. Active development continues on organisation diplomacy, agent training, and bug fixes.

---

## Milestone 1: Truly Playable Alpha State

**GitHub Issue:** [#263](https://github.com/OpenApoc/OpenApoc/issues/263)

This milestone defines the minimum requirements for a game with all core mechanics implemented. Completion of this milestone means you can play through most features of the original game in OpenApoc.

### Completed

- [x] Aliens moving from building to building
- [x] Alien eggs/Chrysalis hatching after time and spawning new units (Cityscape)
- [x] Fully implemented city economy (workers, wages, budgets) -- by @idshibanov ([PR #916](https://github.com/OpenApoc/OpenApoc/pull/916))
- [x] Weekly funding for X-COM and each organisation -- by @idshibanov ([PR #980](https://github.com/OpenApoc/OpenApoc/pull/980))
- [x] Organisation and Gang Agents moving between buildings; generation of resulting missions (raiding, storming, war declarations, peace treaties, alliances) -- by @idshibanov (#998, #999, #1000)
- [x] Bribes for organizations
- [x] Vehicle location screen drag-and-drop mechanics -- by redv
- [x] Hover screen for items -- by FranciscoDA
- [x] Transport repaired at base -- by Istrebitel
- [x] Agent Training on base -- by Istrebitel
- [x] Fixes to UFOPaedia display
- [x] Proper transferring of agents and items between bases
- [x] Alert Screen
- [x] UI hover tooltips -- by Supsuper
- [x] Controls for editing text (naming soldiers and other property)

### In Progress / Remaining

- [ ] Agent Training from Battlescape, including slow training of Androids (currently affected by [#997](https://github.com/OpenApoc/OpenApoc/issues/997) with agents training at extremely high rates)
- [ ] Alien infiltration graph screen (simple version without curved lines -- partially implemented)
- [ ] Full Organisation Diplomacy and Relations structure as per original game (or improved), including two-way relationship values with short-term and long-term bias -- **WIP by @idshibanov** ([#996](https://github.com/OpenApoc/OpenApoc/issues/996))
- [ ] Resolve issue [#997](https://github.com/OpenApoc/OpenApoc/issues/997) (Ticks Per Second issue affecting training rates and other time-based calculations)

---

## Milestone 2: Beta State (All Features Implemented)

**GitHub Issue:** [#264](https://github.com/OpenApoc/OpenApoc/issues/264)

This milestone covers full feature implementation, making OpenApoc a complete (if not yet fully polished) recreation of the original game.

### Completed

- [x] Nightly Score and Finances screen (given at 00:00:00 hours)
- [x] Weekly Funding Assessment screen
- [x] Implementation of Agent medals and per-battle/inter-battle statistics ([#1212](https://github.com/OpenApoc/OpenApoc/issues/1212))
- [x] Organisations making treaties, raiding, storming each other and X-COM with vehicles and agents/gang members
- [x] Message history screen auto-scrolling to newest message ([#546](https://github.com/OpenApoc/OpenApoc/issues/546))
- [x] Camera follow in Geoscape only when craft's tab selected ([#600](https://github.com/OpenApoc/OpenApoc/issues/600))
- [x] Removed the extra two unequipped agents at game start (original game has 10, OpenApoc had 12)
- [x] Main Menu "Options" button renamed (was counter-intuitively linking to Developer Functions)

### In Progress / Remaining

- [ ] Update GitHub and Appveyor to properly label builds with a recognisable version structure for bug reporting
- [ ] Resolve the Ticks Per Second issue in [#997](https://github.com/OpenApoc/OpenApoc/issues/997) to fix erroneous calculations
- [ ] Victory and Defeat screens
- [ ] Alien Takeover screen
- [ ] Proper portal locations in the Alien Dimension
- [ ] Proper portal movement in the Cityscape (with option for weekly or daily movement)
- [ ] Full Graphs and Stats feedback
- [ ] Implement proper Collapse Algorithm for Alien Umbilical in the Alien Dimension
- [ ] Stop alien UFO growth when applicable building is destroyed
- [ ] "UFO Mushrooms" outside alien buildings for visual feedback on next week's UFO spawn
- [ ] Implementation of the Overspawn
- [ ] Organisations buying and selling vehicles according to funds, relationships, and missions ([#1053](https://github.com/OpenApoc/OpenApoc/issues/1053))
- [ ] Organisations sending illegal flyers on attack missions according to relationships (#999, #1000)
- [ ] Organisations ordering craft to retreat when heavily damaged; other AI improvements
- [ ] True ground vehicle movement (lanes, highways, blocking, overtaking) ([#785](https://github.com/OpenApoc/OpenApoc/issues/785))
- [ ] "Drive on right/left" road option and associated pathfinding ([#785](https://github.com/OpenApoc/OpenApoc/issues/785))
- [ ] Full Dynamic Action Music structure with intelligent mixing logic ([#618](https://github.com/OpenApoc/OpenApoc/issues/618))
- [ ] Modding support for Dynamic Music ([#618](https://github.com/OpenApoc/OpenApoc/issues/618))
- [ ] OpenApoc OST Mod completion and distribution
- [ ] Daily screen report (event ordering issues at 00:00:00)
- [ ] onHover for child controls in transaction screen ([#216](https://github.com/OpenApoc/OpenApoc/issues/216))
- [ ] Fix or hide Skirmish Mode (currently has significant bugs)
- [ ] Fix developer name agent equipment loadouts to use Week 1 equipment only
- [ ] Add pre-game Options Menu to Main Menu
- [ ] Keyboard shortcut rebinding
- [ ] UFO "Apocalypse" Mission after control centre is destroyed (all remaining UFOs sent on city-wide attack)
- [ ] Large UFO Attack/Bombing Mission after first entry into alien dimension

---

## Milestone 3: Release 1.0

**GitHub Issue:** [#265](https://github.com/OpenApoc/OpenApoc/issues/265)

This milestone defines what is needed for OpenApoc to be feature-complete compared to the original game and ready for a 1.0 release.

### Feature-Complete vs. Original Game

- [ ] Better Unit AI (see UnitAI forum thread)
- [ ] Battle AI advanced behaviour in evasive and normal mode: using cover, searching for cover, crouching, ducking, crawling, jumping, throwing grenades, diversionary assaults, flanking, strafing
- [ ] Battle AI: Evasive Mode -- agents seek safety and cover, avoiding confrontation
- [ ] Battle AI: Normal Mode -- agents use cover and engage with caution
- [ ] Battle AI: Aggressive Mode -- agents ignore risks and aggressively seek confrontation
- [ ] Battle AI: Wounded agents have penalty to moving and shooting
- [ ] Battle AI: Wounded agents attempt to use medkits in cover
- [ ] Battle AI: More intelligent hostile attack patterns (crawling under fire, smoke grenades, retreat, regroup)
- [ ] Improved Cityscape AI (dynamic response to threats and relations)
- [ ] Improved alien movement within the city (targeting infiltration targets, using friendly organisations to host eggs)
- [ ] Alien movement adhering to travel-time restrictions (not instant teleportation)
- [ ] Retention of agents assigned to certain vehicles in assignment screens
- [ ] Full agent name generator (male/female/unisex first names and last names)
- [ ] Coloured Text Support

### Additional 1.0 Requirements

- [ ] New file format for savegames (replacing XML for faster save/load times) ([#150](https://github.com/OpenApoc/OpenApoc/issues/150))
- [ ] Separation of "rules" and "gamestate" (enabling mid-game mod addition/removal without losing progress)
- [ ] Close all issues relating to Original Game features
- [ ] Any remaining blockers to matching or improving upon Original Game functionality

---

## Extra Features and Quality of Life

**GitHub Issue:** [#941](https://github.com/OpenApoc/OpenApoc/issues/941)

This issue tracks enhancements, modding functions, and quality-of-life updates that are handled separately from the main development milestones. These include improvements that enhance the original game or serve niche/veteran player needs.

### Key Items

**Gameplay Enhancements:**
- [ ] Agent and Vehicle sorting by parent base and vehicle name ([#686](https://github.com/OpenApoc/OpenApoc/issues/686))
- [ ] Display, Object, and UI scaling for high-resolution displays ([#1040](https://github.com/OpenApoc/OpenApoc/issues/1040))
- [ ] Configurable maximum vehicles in raids (#999)
- [ ] Infinite production and "Auto-Sell" button (similar to OpenXCOM)
- [ ] Alien life-cycle working in both Cityscape and Battlescape ([#935](https://github.com/OpenApoc/OpenApoc/issues/935))
- [ ] Improved building security, gangs, and militia as separate factions ([#864](https://github.com/OpenApoc/OpenApoc/issues/864))
- [ ] Close Quarter Combat and Melee System overhaul
- [ ] Organisation-specific coloured vehicles ([#774](https://github.com/OpenApoc/OpenApoc/issues/774))
- [ ] Vehicle module weapon guidance system (`<guided>` tag support) ([#1035](https://github.com/OpenApoc/OpenApoc/issues/1035))
- [ ] Gas Weight and Gas Density system for gaseous damage types
- [ ] Different scaling factors for Cityscape and Battlescape

**Engine and Technical:**
- [ ] Replace tinyfmt with fmt ([#773](https://github.com/OpenApoc/OpenApoc/issues/773))
- [ ] Remove Boost dependencies ([#674](https://github.com/OpenApoc/OpenApoc/issues/674), [#675](https://github.com/OpenApoc/OpenApoc/issues/675), [#676](https://github.com/OpenApoc/OpenApoc/issues/676), [#677](https://github.com/OpenApoc/OpenApoc/issues/677), [#678](https://github.com/OpenApoc/OpenApoc/issues/678))
- [ ] Better save file format ([#150](https://github.com/OpenApoc/OpenApoc/issues/150))

**Completed:**
- [x] Sound throttling for similar sounds ([#197](https://github.com/OpenApoc/OpenApoc/issues/197))
- [x] Screenshots saved with creation date and build info ([#610](https://github.com/OpenApoc/OpenApoc/issues/610))

---

## Summary of Progress

| Milestone | Total Items | Completed | Remaining |
|---|---|---|---|
| Alpha (#263) | 19 | 15 | 4 |
| Beta (#264) | 35 | 8 | 27 |
| Release 1.0 (#265) | 18 | 0 | 18 |
| Extra/QoL (#941) | ~25 | 2 | ~23 |

The Alpha milestone is nearing completion, with the main blockers being agent training issues (tied to the Ticks Per Second bug in [#997](https://github.com/OpenApoc/OpenApoc/issues/997)) and the organisation diplomacy system. The Beta milestone has significant work remaining in areas such as AI, dynamic music, ground vehicle pathfinding, and alien dimension mechanics.

---

## How to Contribute

OpenApoc welcomes contributions. Key areas where help is needed include:

- **Unit AI and Battle AI** -- The largest remaining work item across all milestones
- **Ground vehicle pathfinding** -- Lane-based movement system ([#785](https://github.com/OpenApoc/OpenApoc/issues/785))
- **Dynamic music** -- Implementing the original game's adaptive music system ([#618](https://github.com/OpenApoc/OpenApoc/issues/618))
- **Bug fixes** -- Many issues are tagged with "Help Wanted" on the GitHub issue tracker
- **Testing and bug reporting** -- Playing the game and reporting issues helps prioritize fixes

See the [OpenApoc GitHub repository](https://github.com/OpenApoc/OpenApoc) for the full issue list and contribution guidelines.

---

Sources:
- [Issue #263 - Alpha State](https://github.com/OpenApoc/OpenApoc/issues/263)
- [Issue #264 - Beta State](https://github.com/OpenApoc/OpenApoc/issues/264)
- [Issue #265 - Release 1.0](https://github.com/OpenApoc/OpenApoc/issues/265)
- [Issue #941 - Extra Features and QoL](https://github.com/OpenApoc/OpenApoc/issues/941)
