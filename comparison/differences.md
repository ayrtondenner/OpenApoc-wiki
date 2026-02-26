# Differences to X-COM: Apocalypse

**OpenApoc** is an open-source C++17 reimplementation of [X-COM: Apocalypse](https://www.ufopaedia.org/index.php?title=Apocalypse) (1997). While aiming to faithfully recreate the original game, OpenApoc introduces many improvements, bug fixes, and new features. All new gameplay features are **optional** and can be toggled through the **More Options** menu.

This page documents the known differences between OpenApoc and the original game. For general OpenApoc information, see the [OpenApoc](https://www.ufopaedia.org/index.php/OpenApoc) main page.

## Technical Improvements

OpenApoc runs natively on modern hardware and operating systems, removing the need for DOS emulation:

- **Platform support**: Windows (MSVC 2019+), Linux (GCC 8+/Clang 7+), and macOS (including Apple Silicon)
- **Modern resolutions**: Supports any screen resolution and display scaling, with windowed, fullscreen, and borderless modes
- **Performance**: Runs at 60 FPS with OpenGL 2.0+ / GLES 3.0 rendering
- **Human-readable save games**: Game state is stored as XML in ZIP archives, editable with any text editor
- **Mod support**: Full modding via XML data files, Lua scripting, and a configurable mod loading system
- **Multi-monitor support**: Can be placed on any display in multi-monitor setups
- **Configurable audio**: Separate volume controls for music and sound effects

## New Gameplay Options

All new gameplay features are accessible through the **More Options** menu and can be individually enabled or disabled. Default values are listed -- **ON** means the feature is enabled by default in OpenApoc.

### Cityscape Options

| Option | Description | Default |
|--------|-------------|---------|
| Improved city control scheme | Completely new control scheme with modifier keys (see [Improved Controls](#improved-controls) section). Can be disabled to restore vanilla controls. | ON |
| Ferry checks relationship when buying | Transtellar checks its relationship with X-COM before providing transport services | ON |
| Allow manual use of teleporters in city | Players can manually route vehicles through teleporter buildings for quick transport | ON |
| Allow manual ferrying of cargo and non-combatants | Manual control over ferry transport of cargo and non-combat personnel | ON |
| Allow soldiers to call taxi | Soldiers can use taxis for transport (restricted to civilians in the original) | ON |
| Allow attacking owned vehicles | Allows X-COM to attack its own vehicles (impossible in the original game) | ON |
| Call existing transport instead of spawning them | Reuses existing transport vehicles instead of spawning new ones | ON |
| Attempt to recover agent equipment dropped in city | Equipment dropped by agents in the city is automatically recovered | ON |
| Enforce vehicle cargo limits | Strict enforcement of vehicle cargo capacity | OFF |
| Allow nearby vehicles to pick up loot | Nearby X-COM vehicles can collect loot from crash sites | ON |
| Allow loot to be stashed in the building | Recovered loot can be deposited in buildings | ON |
| Armored roads | Roads have damage reduction, making them harder to destroy | ON |
| Unsupported ground vehicles crash | Ground vehicles without road support will crash (weapons and modules may be lost) | ON |
| Vehicles crash when entering dimension gates | Vehicles incapable of dimensional travel crash when entering gates | ON |
| Vehicles crash when out of fuel | Vehicles crash when their fuel runs out | ON |
| Successful raid collapses building | Buildings collapse after a successful raid | OFF |
| Any hit on hostile building provokes retaliation | Stray shots hitting hostile buildings trigger retaliation | OFF |
| Put market stock on the right side | Market stock displayed on the right side of the transaction screen | ON |
| Left clicking icon opens equip menu | Left-clicking a unit's icon opens the equipment screen | OFF |
| Skip turbo movement calculations | Performance optimization that skips turbo movement math | OFF |
| Allow ATVs to initiate UFO recovery missions | All Terrain Vehicles can start UFO recovery missions | ON |
| Show vehicles in current dimension only | Vehicle list filters to show only the current dimension | ON |
| Add prefix to non-X-COM vehicles | Non-X-COM vehicles are prefixed with * in vehicle lists for easy identification | ON |
| Don't follow vehicles in strategy view | Disables automatic camera following in strategy (isometric) view | OFF |
| Use currency formatting | Monetary values displayed with currency formatting (e.g., $1,234,567) | ON |

### Battlescape Options

| Option | Description | Default |
|--------|-------------|---------|
| Explosions damage instantly | Explosions cause damage immediately rather than with a delay | ON |
| X-Com 1 (UFO) Damage model (0-200%) | Uses the [UFO: Enemy Unknown](https://www.ufopaedia.org/index.php?title=UFO:_Enemy_Unknown) damage randomization model (0-200% of base damage) instead of Apocalypse's model | OFF |
| Gravlift sounds | Sound effects play when units enter or exit gravlifts | ON |
| Throwing requires proper facing and pose | Units must face the target and be in the correct stance before throwing | ON |
| Ammunition explodes when blown up | Carried ammunition detonates when a unit or vehicle is destroyed | ON |
| Display unit paths in battle | Movement paths are visually displayed during tactical combat | ON |
| Display additional unit icons (fatal, psi) | Extra status icons shown for fatal wounds and psionic effects | ON |
| Allow force-firing parallel to the ground | Force-fire mode allows shots aimed parallel to the ground plane | ON |
| Require LOS to maintain psi attack | Psionic attacks require maintained line of sight to the target | OFF |
| Hitting vehicle shield produces alternate sound | Different sound effect when vehicle shields absorb damage | ON |
| All units run and kneel by default | Units default to running movement and kneeling stance | ON |
| Automatically reload weapons when empty | Weapons auto-reload from carried ammunition when a clip is expended | ON |
| Weapons autoreload only same ammo type | Auto-reload only uses the same ammunition type that was previously loaded | ON |
| Mousewheel changes vertical level in battlescape | Mouse scroll wheel changes the displayed map level | ON |
| Select squad with single click | Single-click squad number buttons to select the entire squad | OFF |
| Disable scrolling sounds | Turns off the sound effect when scrolling the map | OFF |

### General Options

| Option | Description | Default |
|--------|-------------|---------|
| Show debug commands on screen | Displays debug/cheat command buttons in the interface | ON |
| Allow unloading clips and quick equip | Advanced inventory controls: Shift+click for auto-equip, Ctrl+click to remove clips | ON |
| Enable agent equipment templates | Save and load agent equipment loadouts with number keys (Ctrl+1-0 to save, 1-0 to apply) | ON |
| Seed RNG on game start | Seeds the random number generator at game start for varied gameplay | ON |
| Enable mouse capture for the window | Captures the mouse cursor within the game window | OFF |

### Mod Options

| Option | Description | Default |
|--------|-------------|---------|
| Max tile repair per night | Maximum number of scenery tiles construction vehicles repair each night (0-100) | 5 |
| Scenery repair cost factor | Percentage of original price organizations pay for scenery repair (0-100%) | 10% |
| Stunning hurts relationships | Stunning units belonging to an organization damages X-COM's relationship with them | OFF |
| Initiating raid hurts relationships | Starting a raid on a building damages the relationship with its owner | OFF |
| (MOD) Original Brainsucker Launcher SFX | Uses the original game's Brainsucker Launcher sound effect | ON |
| (MOD) Invulnerable roads | Roads cannot be damaged or destroyed | OFF |
| (MOD) Griffon becomes All-Terrain | The Griffon AFV becomes an all-terrain vehicle capable of off-road movement | ON |
| (MOD) Wolfhound APC becomes All-Terrain | The Wolfhound APC becomes an all-terrain vehicle | ON |
| Vehicles crash on low HP | Vehicles crash when their health drops critically low (weapons and modules may be lost) | OFF |

### Cheat Options

OpenApoc provides a dedicated cheat menu not present in the original game:

| Option | Description | Default |
|--------|-------------|---------|
| Infinite ammo | Unlimited ammunition for all X-COM agents and vehicles | OFF |
| Damage inflicted multiplier | Multiplier for damage dealt by X-COM (0x - 5x) | 1.0x |
| Damage received multiplier | Multiplier for damage taken by X-COM (0x - 5x) | 1.0x |
| Hostiles multiplier | Multiplier for the number of hostile units spawned (0.5x - 3x) | 1.0x |
| Stat growth multiplier | Multiplier for agent stat growth rate (0x - 99.5x) | 1.0x |

Additional cheat buttons: Give All Research, Make All Orgs Friendly/Hostile, Make All Orgs Utopia/Chaos, Modify Funds, Set Time Before Midnight, Fast Forward to End of Day/Week/Month.

## Improved Controls

The original game's city controls were inconsistent and limited. OpenApoc introduces a completely new control scheme using modifier keys. This can be disabled via the "Improved city control scheme" option to restore vanilla behavior.

### Cityscape Mouse Controls

| Input | Action |
|-------|--------|
| Left Click on building | Open building screen (base screen if building contains a base) |
| Right Click on building | Open building screen |
| Shift + Left Click | Order attack vehicle |
| Shift + Right Click | Order follow vehicle / go to location |
| Alt + Shift + Left Click | Order attack building |
| Alt + Shift + Right Click | Order go to building |
| Alt + Left Click | Open UFOpaedia for object (vehicle type, building function, projectile source) |
| Alt + Right Click | Open UFOpaedia for object's owner |
| Ctrl + move order (agents) | Force agents to move on foot (never call taxi), allows personal teleporter use |
| Ctrl + move order (vehicles) | Allows manual use of city teleporters |
| Ctrl + attack order | Forces vehicles to attack target (instead of UFO recovery or escort) |
| Ctrl + Left Click (selection) | Add unit/vehicle to selection (additive selection) |
| Right Click (selection) | Remove unit/vehicle from selection |
| Middle Click | Move camera to location |

### Cityscape Mouse on Vehicle/Agent Icons

| Input | Action |
|-------|--------|
| Shift + Right Click | Open location screen |
| Ctrl + Shift + Right Click | Open equipment screen |
| Alt + Shift + Right Click | Open equipment screen |

### Agent Equipment Controls

| Input | Action |
|-------|--------|
| Shift + Click | Auto-equip item to first available slot, or auto-remove to stores/ground |
| Ctrl + Click on weapon | Remove clip from weapon |
| 1-0 | Apply saved equipment template to all selected agents |
| Ctrl + 1-0 | Save current agent's equipment set as a template |

### Battlescape Mouse Controls

| Input | Action |
|-------|--------|
| Left Click | Order unit to execute action (move/throw/psi/teleport), open probed unit screen, use item |
| Right Click | Turn towards cursor, focus enemy (real-time), use item auto-function (e.g., prime grenade for impact) |
| Shift + Left Click | Force-fire at target tile, shot parallel to ground |
| Shift + Alt + Left Click | Force-fire at target tile, shot aimed at tile's ground |
| Alt + move order | Unit keeps facing target while moving (strafe/backpedal) |
| Ctrl + Left Click | Add unit to selection (additive) |
| Right Click | Remove unit from selection |

### Battlescape Keyboard

| Key | Action |
|-----|--------|
| PgUp / PgDown | Change map levels |
| V | Toggle layering |
| F2-F4 | Movement modes: Prone / Walk / Run |
| F5-F8 | Fire modes: Cease / Aimed / Snap / Auto |
| F9-F11 | Behavior: Evasive / Normal / Aggressive |
| Backspace | Toggle kneel |
| 1-6 | Select squad |
| Shift + 1-6 | Select specific unit in current squad |
| Shift + Ctrl + 1-6 | Add unit to selection |
| Alt + 1-6 | Cycle through spotted enemies of unit |
| Enter | Open inventory |
| [ / ] | Throw right / left hand item |
| ' / \ | Drop right / left hand item |
| E | End turn (turn-based mode) |
| J | Make unit jump (down from a cliff) |
| S / L | Open save / load menu |

### General Controls

| Key | Action |
|-----|--------|
| Mousewheel | Scroll lists |
| Esc | Go back, close form, cancel |
| Enter | Confirm, go forward |
| Space | Pause/Resume time |
| Tab | Toggle map |
| C | Toggle follow mode |
| M | Show message log |
| Home | Zoom to last event |
| Arrows | Move camera |
| 0-5 (Cityscape) | Control game speed |

## Pause Notifications

OpenApoc adds a comprehensive **configurable notification system** that can pause the game when specific events occur. Each notification can be individually toggled. These are not present in the original game.

### City Notifications

- UFO spotted
- Vehicle damage (light / moderate / heavy / destroyed)
- Vehicle escaping (damaged and returning to base)
- Vehicle out of ammo
- Vehicle low on fuel
- Agent died
- Agent arrived at base
- Cargo / Transfer / Recovery arrived at base
- Vehicle repaired / rearmed / refuelled
- Not enough ammo / fuel
- Unauthorized vehicle detected
- X-COM base destroyed

### Battle Notifications

- Hostile spotted / died
- Unknown unit died
- Agent died / brainsucked
- Agent critically wounded / badly injured / injured
- Agent under fire
- Agent unconscious / left combat zone
- Agent frozen / berserk / panicked / panic over
- Psionic attack on unit / unit under psionic control / freed from control

## Original Game Bugs Fixed

OpenApoc fixes or avoids several [known bugs](https://www.ufopaedia.org/index.php?title=Known_Bugs_(Apocalypse)) from the original game:

- **UFO speed bug**: Fixed alien craft having 0 speed in certain conditions
- **Infiltration screen overflow**: Fixed infiltration screen going blank when exceeding 42 days
- **Security Station turrets** (partial): In the original turn-based mode, Security Station turrets did not have their TUs refreshed at the start of turns, rendering them mostly useless after the first shot
- **Sound issues**: Fixed OGG Vorbis music playback issues that could occur in the original
- **Learning AI**: The original game's advertised "learning AI" was effectively non-functional -- it stopped working after saving the game and depended on specific CD-ROM file locations. OpenApoc does not attempt to replicate this broken feature
- **Brainsucker Pod handling**: Various fixes for Brainsucker Pod inventory issues, storage space, and alien containment display

## Modding Support

Unlike the original game, OpenApoc is designed with modding in mind:

- **XML data files**: Nearly all game data (units, weapons, vehicles, buildings, organizations) is defined in editable XML files
- **Mod loading system**: Mods are loaded from a configurable directory (default: `./data/mods`), specified as a colon-separated list
- **Lua scripting**: A Lua scripting system allows custom AI and game logic modifications. Scripts are loaded via the `OpenApoc.Mod.ScriptsList` configuration option
- **Editable save games**: Since saves are XML in ZIP archives, game state can be manually edited

## Features Not Yet Implemented

As of early 2026, OpenApoc is in **alpha** state. The following features from the original game are not yet fully implemented:

### Core Gameplay

- Victory and defeat screens
- Alien Takeover screen
- Full organization diplomacy with dual relationship values (the original tracked two separate relationship scores per organization)
- Overspawn mechanic
- Full dynamic action music structure
- Agent name generator

### AI and Movement

- Advanced battle AI: cover usage, flanking, grenade throwing, retreat and regrouping behaviors
- Intelligent alien movement patterns within the city
- True ground vehicle movement with lanes, highways, and overtaking behavior
- Evasive/Normal/Aggressive unit AI behavior modes (buttons exist but AI differentiation is incomplete)

### Other

- Proper portal locations in the Alien Dimension
- Full graphs and statistics feedback screens
- Organization vehicle AI (buying, selling, managing their own fleets)
- Coloured text support in some UI elements

For the full development roadmap, see the [Playable Alpha](https://github.com/OpenApoc/OpenApoc/issues/263), [Beta](https://github.com/OpenApoc/OpenApoc/issues/264), and [Release 1.0](https://github.com/OpenApoc/OpenApoc/issues/265) milestone issues on GitHub.

## Debug Mode

OpenApoc includes an extensive debug system not present in the original game. Debug hotkeys are toggled with **F1** in both the cityscape and battlescape. When enabled, various diagnostic and cheat functions become available:

### Cityscape Debug

- Ctrl+Alt+Shift+Click: Destroy scenery / collapse building
- Spawn UFOs, repair scenery, warp to alien dimension
- Display road pathfinding, walk modes, alien positions, vehicle paths
- Dump voxel maps for line of sight/fire analysis
- Highlight tubes, roads, and hills with directional filters

### Battlescape Debug

- Teleport units, stun/remove units, restore stats
- Reveal entire map with line-of-sight visualization
- Modify morale and psionic stats
- Spawn explosions and directional shots
- Re-link support lines for map parts

### Base Screen Debug

- Instantly finish all facility construction
- Near-instantly complete research projects

## See Also

- [OpenApoc](https://www.ufopaedia.org/index.php/OpenApoc) -- main OpenApoc page
- [X-COM: Apocalypse](https://www.ufopaedia.org/index.php?title=Apocalypse) -- original game page
- [Known Bugs (Apocalypse)](https://www.ufopaedia.org/index.php?title=Known_Bugs_(Apocalypse)) -- bugs in the original game
- [OpenApoc on GitHub](https://github.com/OpenApoc/OpenApoc) -- source code and issue tracker
- [README_HOTKEYS.txt](https://github.com/OpenApoc/OpenApoc/blob/master/README_HOTKEYS.txt) -- complete hotkey reference
