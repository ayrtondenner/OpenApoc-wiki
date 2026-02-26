# Modding Guide

**Modding** is a core design goal of OpenApoc. Nearly every aspect of the game -- weapons, vehicles, organisations, research, maps, difficulty settings, economy, and more -- is defined in human-readable XML data files that can be overridden or extended by mods. OpenApoc also includes a **Lua scripting** system that allows mods to hook into game events and alter game logic at runtime.

This page covers the mod system architecture, the data file format, savegame editing, Lua scripting, configurable mod options, and how to create your own mods.

---

## Mod System Overview

OpenApoc loads game data in layers. The base game data is extracted from the original X-COM: Apocalypse CD image, then OpenApoc's own data patches are applied on top, and finally any enabled mods are loaded in order. Each layer can add new data or override existing values from previous layers.

### How Mods Are Loaded

Mod loading is controlled by two configuration options (found in `settings.cfg` or set via the launcher):

- **`Game.Mods`** -- A colon-separated list of mod directory names to load (relative to the mod directory). Default: `base`
- **`Game.ModPath`** -- The directory containing all mods. Default: `./data/mods`

When the game starts, it iterates through the mod list in order. For each mod it:

1. Reads `modinfo.xml` from the mod's root directory
2. Appends the mod's **data path** to the virtual filesystem (making the mod's resources available and able to override earlier files)
3. Loads the mod's **game state** (XML data that gets merged into the running GameState)
4. Loads any **language patches** applicable to the current locale
5. Executes the mod's **load script** (a Lua script run when the mod is first loaded)

Because mods are loaded in the order specified, later mods override earlier ones. The `base` mod is the foundation and should generally always be listed first.

### The Launcher

The OpenApoc Launcher (a Qt-based GUI) includes a **Mods** tab that lets you enable and disable mods without manually editing configuration files. It scans the `data/mods/` directory for subdirectories containing a valid `modinfo.xml` and displays them in two lists: enabled mods and disabled mods. You can move mods between the lists and reorder them.

---

## The modinfo.xml File

Every mod must contain a `modinfo.xml` file in its root directory. This file describes the mod's metadata and tells OpenApoc how to load it. Here is the structure, using the base game mod as an example:

```xml
<?xml version="1.0"?>
<openapoc_modinfo>
    <name>OpenApoc base game</name>
    <author>OpenApoc team</author>
    <version>0.1</version>
    <description>The base OpenApoc game</description>
    <link>http://www.openapoc.org</link>
    <id>org.openapoc.base</id>
    <datapath>data</datapath>
    <statepath>base_gamestate</statepath>
    <minversion></minversion>
    <modloadscript>scripts/org.openapoc.base/onload.lua</modloadscript>
    <requires />
    <conflicts />
    <languages>
        <entry>
            <ID>en.UTF-8</ID>
            <patch></patch>
            <data>lang/data/en.UTF-8</data>
        </entry>
    </languages>
</openapoc_modinfo>
```

### Field Reference

| Field | Description |
|---|---|
| `name` | The human-readable name of the mod, displayed in the launcher. |
| `author` | The author(s) of the mod. |
| `version` | A version string (any format; purely informational). |
| `description` | A short description of what the mod does. |
| `link` | A URL for the mod's homepage, forum thread, etc. |
| `id` | A **unique** identifier for the mod. Use a reverse-DNS-like format to avoid conflicts, e.g. `org.openapoc.mod.YOUR_USERNAME.YOUR_MOD`. |
| `datapath` | Path (relative to the mod directory) to a folder whose contents are added to the virtual filesystem. Files here can override any game resource (images, sounds, forms, etc.). |
| `statepath` | Path (relative to the mod directory) to a folder or ZIP archive containing XML game state data to merge into the GameState. |
| `minversion` | The minimum version of OpenApoc required to run this mod (currently informational). |
| `modloadscript` | Path to a Lua script that is executed when the mod is loaded (after game state is merged). |
| `requires` | A list of mod IDs that this mod depends on. Listed as `<entry>mod.id</entry>` elements. |
| `conflicts` | A list of mod IDs that this mod is incompatible with. |
| `languages` | Language-specific data and translation patches. Each entry has an `ID` (locale), optional `patch` (game state overlay for that language), and optional `data` (additional data path for that language). |

---

## Data File Structure

OpenApoc organises its data in the `data/` directory. Understanding this structure is essential for modding.

### Top-Level Directories

| Directory | Contents |
|---|---|
| `data/common_patch/` | The core game state patch: XML files defining all game objects (weapons, vehicles, organisations, research, etc.). This is the primary source of moddable game data. |
| `data/difficulty0_patch/` through `data/difficulty4_patch/` | Difficulty-specific overrides applied on top of the common patch. Each corresponds to a difficulty level (0 = Easiest, 4 = Hardest). |
| `data/resource_patch/` | Additional resource patches. |
| `data/city/` | City-related image resources (map overlays, UI elements, building indicators). |
| `data/battle/` | Battle-related data and resources. |
| `data/maps/` | Map data files. |
| `data/tilesets/` | Tileset definitions for map rendering. |
| `data/forms/` | XML UI form definitions (the layout of menus, screens, and dialogs). |
| `data/fonts/` | Font data files. |
| `data/imagepacks/` | Sprite and image pack data. |
| `data/animationpacks/` | Unit animation pack data. |
| `data/bulletsprites/` | Projectile sprite images. |
| `data/languages/` | Translation files for localisation. |
| `data/scripts/` | Lua scripts loaded by the engine (see [Lua Scripting](#lua-scripting)). |
| `data/mods/` | The mods directory, containing all installed mods. |
| `data/ui/` | UI image resources. |

### Game State XML Files

The game state is defined by a hierarchy of XML files rooted at `gamestate.xml`. The root file uses XInclude (`xi:include`) to pull in individual data files for each object type. The key files in `common_patch/gamestate/` are:

| File | Contents |
|---|---|
| `agent_equipment.xml` | Agent (soldier) weapons, armour, grenades, equipment, and their stats (damage, accuracy, range, weight, etc.). |
| `agent_types.xml` | Agent type definitions (X-COM agents, aliens, civilians, building security, etc.). |
| `agent_body_types.xml` | Physical body type definitions for agents. |
| `agent_generator.xml` | Rules for procedurally generating agents (name lists, stat ranges). |
| `vehicle_types.xml` | Vehicle type definitions (stats, images, type classification such as Road, Flying, ATV, UFO). |
| `vehicle_equipment.xml` | Vehicle weapons and modules (lasers, missiles, engines, shields, etc.). |
| `vehicle_ammo.xml` | Vehicle ammunition definitions (ammo types, capacities, costs). |
| `organisations.xml` | Organisation definitions (Megapol, Marsec, Cult of Sirius, etc.), including relationships, guard types, and hireable agent types. |
| `facility_types.xml` | Base facility definitions (labs, workshops, living quarters, stores, etc.). |
| `research.xml` | The research tree: topics, dependencies, costs, and what they unlock. |
| `damage_types.xml` | Damage type definitions and damage modifiers. |
| `ufopaedia.xml` | UFOpaedia article definitions and categories. |
| `ufo_growth_lists.xml` | UFO spawning rules per week, controlling the alien invasion progression. |
| `ufo_incursions.xml` | UFO incursion event definitions. |
| `ufo_mission_preference.xml` | UFO mission target preferences. |

The root `gamestate.xml` also contains inline data for game-wide settings such as:

- `weekly_rating_rules` -- Score thresholds that affect government funding changes
- `agent_salary` -- Weekly salary per agent role (Soldier, Physicist, BioChemist, Engineer)
- `initial_agents` -- Number of agents per role at game start
- `initial_facilities` -- Starting base facilities
- `initial_agent_equipment` -- Equipment loadouts for starting agents
- `initial_vehicles` -- Starting vehicles and their equipment
- `initial_vehicle_equipment` and `initial_vehicle_ammo` -- Spare vehicle equipment and ammo in starting base storage

### XML Data Format

Game state data uses a consistent key/value format. Collections are stored as lists of `<entry>` elements, where each entry has a `<key>` and a `<value>`. The key is a unique string identifier (e.g. `VEHICLETYPE_PHOENIX_HOVERCAR`, `AEQUIPMENTTYPE_MEGAPOL_LASER_SNIPER_GUN`).

To override an existing object, you only need to provide the key and the specific fields you want to change. Fields you omit will retain their original values. For example, to change only the manufacturer of the Dimension Probe vehicle:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<vehicle_types>
  <entry>
    <key>VEHICLETYPE_DIMENSION_PROBE</key>
    <value>
      <name>Dimension Probe</name>
      <manufacturer>ORG_X-COM</manufacturer>
    </value>
  </entry>
</vehicle_types>
```

---

## Savegame Editing

One of OpenApoc's key features is its human-readable save game format. All save games are stored as **XML files inside a ZIP archive** (with a `.zip` extension, though they may not have one if unpacked saving is enabled).

### Save Location

By default, saves are stored in the `./saves/` directory relative to the OpenApoc installation. This can be changed via the `Game.Save.Directory` configuration option.

### Save Format

The `Game.Save.Pack` option (default: `true`) controls whether saves are packed into ZIP archives or saved as a directory of loose XML files. When packed:

- The save file is a standard ZIP archive
- Inside it are multiple XML files following the same structure as the game state data (one XML file per object category)
- The XML files use the same format as the data patches (described above)

### Editing a Save

To edit a saved game:

1. Locate the save file in the saves directory
2. If it is a ZIP file, extract it using any ZIP-compatible tool (7-Zip, WinRAR, the built-in OS extractor, etc.)
3. Edit the desired XML files with a text editor
4. If you extracted a ZIP, re-compress the files back into a ZIP archive with the same name
5. Load the modified save in OpenApoc

Alternatively, you can set `Game.Save.Pack` to `false` in `settings.cfg`. This causes saves to be written as directories of loose XML files, which makes editing easier since you do not need to extract and repack a ZIP.

Common things to edit in saves include:

- Organisation relationships (in the organisations data)
- Agent stats and equipment
- Vehicle loadouts and positions
- Player funds
- Research progress

> **Tip:** OpenApoc also supports optional CRC and SHA1 checksums on save files (controlled by `Framework.Serialization.CRC` and `Framework.Serialization.SHA1`). If these are enabled, manually editing a save file will invalidate the checksum. By default, both are disabled.

---

## Lua Scripting

OpenApoc integrates **Lua** (bundled as a dependency) as a scripting language. Lua scripts can hook into game events, modify game state at runtime, and implement complex game logic that would be difficult to express in static XML data.

### How Scripts Are Loaded

Scripts are loaded via the `OpenApoc.Mod.ScriptsList` configuration option. This is a **semicolon-separated** list of Lua script paths (resolved through the virtual filesystem). The default value is:

```
scripts/openapoc_base.lua;
```

When the game state is initialised, each script in this list is executed in order. Scripts can use the standard Lua `dofile()` function to include additional scripts.

Additionally, each mod can specify a `<modloadscript>` in its `modinfo.xml`. This script is executed after the mod's game state has been loaded and merged.

### The OpenApoc Lua API

Scripts have access to a global `OpenApoc` table that provides:

**`OpenApoc.GameState`** (commonly aliased as `GS`) -- Direct access to the full game state, including:

| Table | Contents |
|---|---|
| `GS.vehicle_types` | All vehicle type definitions |
| `GS.agent_equipment` | All agent equipment definitions |
| `GS.organisations` | All organisation definitions |
| `GS.vehicle_equipment` | All vehicle equipment definitions |
| `GS.vehicle_ammo` | All vehicle ammo definitions |
| `GS.cities` | City data |
| `GS.vehicles` | Active vehicle instances |
| `GS.agents` | Active agent instances |
| `GS.economy` | Economy data for all items |
| `GS.ufo_growth_lists` | UFO growth/spawning rules |
| `GS.gameTime` | Current game time |
| `GS.rng` | The game's random number generator |
| `GS.player` | Reference to the player organisation |
| `GS.difficulty` | Current difficulty level (0-4) |
| `GS.agent_generator` | The agent generator (can create new agents) |

**`OpenApoc.Framework`** (commonly aliased as `FW`) -- Framework functions:

| Function | Description |
|---|---|
| `FW.LogInfo(message)` | Log an informational message |
| `FW.LogWarning(message)` | Log a warning |

**`OpenApoc.Framework.Config`** (commonly aliased as `CFG`) -- Configuration access:

| Function | Description |
|---|---|
| `CFG.getBool('Section.Key')` | Read a boolean config value |
| `CFG.getInt('Section.Key')` | Read an integer config value |

**`OpenApoc.enum`** -- Game enumerations, e.g.:
- `OpenApoc.enum.VehicleType.Type.ATV`
- `OpenApoc.enum.VehicleType.Type.Road`
- `OpenApoc.enum.VehicleType.Type.UFO`

### Hooks

The scripting system uses a hook-based architecture. Scripts register functions in `OpenApoc.hook` that the engine calls at specific points during gameplay. The available hooks are:

| Hook Name | When It Is Called |
|---|---|
| `newGame` | When a new game is started (before initial state setup). |
| `newGamePostInit` | After the new game's initial state has been fully set up (registered in the base Lua script, not called directly by C++; chained from `newGame` flow). |
| `applyMods` | When mod-related game state changes should be applied (e.g. toggling vehicle types based on config options). |
| `updateEndOfDay` | At the end of each in-game day. |
| `updateEndOfWeek` | At the end of each in-game week (used for economy updates and UFO growth). |

Scripts should chain hooks rather than replace them, preserving any previously registered hook:

```lua
local oldHook = OpenApoc.hook.updateEndOfWeek
OpenApoc.hook.updateEndOfWeek = function()
    if oldHook then oldHook() end
    -- your custom logic here
end
```

### Base Scripts

The default `scripts/openapoc_base.lua` script and its included files implement core game mechanics:

- **`openapoc_base.lua`** -- The main script. Provides utility functions (`pickRandom`, `math.clamp`, `math.round`), seeds the RNG on new game start, applies mod options (ATV vehicle types, brainsucker launcher sound, crashing vehicles), spawns developer Easter egg agents, and chains weekly update hooks.
- **`update_economy.lua`** -- Implements the weekly economy update (item stock fluctuation and price changes, based on Wong's guide).
- **`update_ufo_growth.lua`** -- Implements weekly UFO growth/spawning in the alien dimension, respecting per-week growth lists and vehicle limits.

### Mod Load Scripts

The base mod's load script (`scripts/org.openapoc.base/onload.lua`) demonstrates how a mod load script works:

```lua
local OA = OpenApoc
local GS = OpenApoc.GameState
local FW = OpenApoc.Framework

FW.LogInfo("On load script called")

local gamestateString = "submods/org.openapoc.base/difficulty" .. tostring(GS.difficulty)
FW.LogInfo("Loading difficulty patch" .. gamestateString)

GS.appendGameState(GS, gamestateString)

FW.LogInfo("Finished loading difficulty patch")
```

This script uses the current difficulty level to load a difficulty-specific game state patch from a submod directory, allowing different difficulty settings to override game data (such as organisation relationships, city layouts, and alien forces).

---

## Mod Options

OpenApoc provides several configurable options in the **More Options** menu under the `OpenApoc.Mod` section. These are options that can meaningfully change gameplay balance and are considered "mod-like" changes:

| Option | Type | Default | Description |
|---|---|---|---|
| `MaxTileRepair` | Integer | 5 | Maximum number of scenery tiles that Construction Vehicles will repair per night. |
| `SceneryRepairCostFactor` | Float | 10.0 | Percentage of the original price organisations must pay for scenery tile repairs. |
| `StunHostileAction` | Boolean | false | Whether stunning an organisation's units counts as a hostile action (hurts relationships). |
| `RaidHostileAction` | Boolean | false | Whether initiating a raid on a building counts as a hostile action (hurts relationships). |
| `BSKLauncherSound` | Boolean | true | Use the original Brainsucker Launcher sound effect (instead of the generic powers sound). |
| `InvulnerableRoads` | Boolean | false | Makes road scenery tiles indestructible. |
| `ATVTank` | Boolean | true | Makes the Griffon AFV an All-Terrain Vehicle (can travel on roads and fly). |
| `ATVAPC` | Boolean | true | Makes the Wolfhound APC an All-Terrain Vehicle. |
| `CrashingVehicles` | Boolean | false | Vehicles crash when their HP drops below 1/7 of maximum (weapons and modules may be lost). |
| `ScriptsList` | String | `scripts/openapoc_base.lua;` | Semicolon-separated list of Lua scripts to load at game initialisation. |

These options are applied at runtime through the Lua scripting system (in the `applyMods` hook), so their effects take place each time a game is loaded or started. This means you can change these options between play sessions without starting a new game.

---

## Creating a Mod

### Basic Steps

1. **Create a mod directory** inside `data/mods/`. Choose a descriptive name (e.g. `my_balance_mod`).
2. **Create a `modinfo.xml`** file in your mod's root directory (see the [modinfo.xml reference](#the-modinfoxml-file) above).
3. **Choose a unique ID** for your mod using reverse-DNS format: `org.openapoc.mod.your_name.mod_name`.
4. **Create a data directory** (referenced by `<datapath>` in your modinfo.xml) for any resource overrides.
5. **Create a game state directory** (referenced by `<statepath>`) containing XML files that override or extend the base game state.
6. **Optionally create Lua scripts** for dynamic logic (referenced by `<modloadscript>`).
7. **Enable your mod** by adding its directory name to the `Game.Mods` option (colon-separated), or by enabling it in the launcher.

### Mod Directory Structure

A typical mod directory might look like this:

```
data/mods/my_mod/
    modinfo.xml                          -- Mod metadata and configuration
    my_gamestate/                        -- Game state overrides (referenced by <statepath>)
        gamestate.xml                    -- Root game state file with xi:include references
        gamestate/
            agent_equipment.xml          -- Override agent equipment stats
            vehicle_types.xml            -- Override vehicle stats
            organisations.xml            -- Override organisation data
    data/                                -- Data path overrides (referenced by <datapath>)
        scripts/
            my_mod/
                onload.lua               -- Mod load script
        submods/
            my_mod/
                custom_patch/            -- Additional game state loaded by scripts
```

### Tips

- You only need to include the XML fields you want to change. Unspecified fields retain their original values.
- Use the `common_patch/gamestate/` files as a reference for available fields and their expected format.
- The game state is loaded cumulatively: the base data is loaded first (from the original CD and the extractor), then `common_patch`, then difficulty patches, then mods in order. Your mod's changes are layered on top of all previous data.
- Files in your mod's `<datapath>` directory override files with the same relative path from earlier in the load order. This lets you replace images, sounds, form definitions, and other resources.
- Test changes incrementally. Start by modifying a single value (e.g. a weapon's damage) and verify it works before making larger changes.
- Keep your mod's files under a directory named after your mod ID to avoid filename conflicts with other mods.

---

## Examples

### Changing a Weapon's Stats

To increase the damage of the Megapol Laser Sniper Gun, create a file in your mod's game state directory:

```xml
<!-- agent_equipment.xml -->
<?xml version="1.0" encoding="UTF-8"?>
<agent_equipment>
  <entry>
    <key>AEQUIPMENTTYPE_MEGAPOL_LASER_SNIPER_GUN</key>
    <value>
      <damage>40</damage>
      <accuracy>85</accuracy>
    </value>
  </entry>
</agent_equipment>
```

### Making a Vehicle All-Terrain via Lua

The base game already demonstrates this pattern. In your mod's Lua script:

```lua
local OA = OpenApoc
local GS = OpenApoc.GameState

local oldApplyMods = OpenApoc.hook.applyMods
OpenApoc.hook.applyMods = function()
    if oldApplyMods then oldApplyMods() end

    -- Make the Phoenix Hovercar an ATV
    GS.vehicle_types['VEHICLETYPE_PHOENIX_HOVERCAR'].type = OA.enum.VehicleType.Type.ATV
end
```

### Modifying Organisation Relationships

To change starting organisation data, override the organisations XML:

```xml
<!-- organisations.xml -->
<?xml version="1.0" encoding="UTF-8"?>
<organisations>
  <entry>
    <key>ORG_MEGAPOL</key>
    <value>
      <average_guards>15</average_guards>
    </value>
  </entry>
</organisations>
```

### Adding a Weekly Event via Lua

```lua
local OA = OpenApoc
local GS = OpenApoc.GameState
local FW = OpenApoc.Framework

local oldWeekHook = OpenApoc.hook.updateEndOfWeek
OpenApoc.hook.updateEndOfWeek = function()
    if oldWeekHook then oldWeekHook() end

    local week = GS.gameTime:getWeek()
    FW.LogInfo("Custom mod: Week " .. tostring(week) .. " has ended!")
    -- Add your custom weekly logic here
end
```

### Modifying Starting Loadouts

The `common_patch/gamestate.xml` file defines `initial_agent_equipment`, `initial_vehicles`, and `initial_vehicle_equipment`. You can override these in your mod to give the player different starting equipment, vehicles, or base facilities.

---

## The Base Mod

The `base` mod (`data/mods/base/`) is OpenApoc's foundational mod that ships with the game. It provides:

- **Game state data** in `base_gamestate/` (the initial game state loaded on top of the extracted CD data and common patches)
- **Music playlists** in `data/playlists/` (city, tactical, action, and alien dimension music)
- **Difficulty submods** in `data/submods/org.openapoc.base/` (difficulty0 through difficulty4, loaded dynamically based on the selected difficulty)
- **A mod load script** (`data/scripts/org.openapoc.base/onload.lua`) that applies difficulty-specific patches at load time
- **Language support** with locale-specific data paths

The base mod should generally always be enabled and listed first in the mod load order, as other mods are designed to layer on top of it.

---

## Community Research Findings

The following sections contain additional modding knowledge gathered from the OpenApoc Discord community. These insights supplement the official documentation above and reflect practical experience from active modders and contributors.

### Data File Architecture and Load Order

The XML data system uses a strict layered loading architecture where order matters (source: Discord community, skin36, filmboy84):

1. **Generated data** -- Extracted from the original CD ISO by the extractor tools.
2. **`common_patch`** -- Applied on top of generated data, providing OpenApoc's baseline corrections and additions.
3. **Difficulty-specific patch** (`difficulty0_patch` through `difficulty4_patch`) -- Overrides for the selected difficulty level.
4. **Mod patches** -- Loaded in the order specified by `Game.Mods`.

**Critical caveat**: Difficulty patches load AFTER mods in the current architecture. This means mods cannot directly override difficulty-specific values through XML alone. The workaround is to use **Lua `onload` scripts** (as demonstrated by PR #783) which execute at load time and can programmatically apply difficulty-aware changes. The base mod already uses this pattern to load difficulty patches via `onload.lua`.

### The gamestate_common Archive

The `gamestate_common` file is a **ZIP archive with no file extension**. This catches many new modders off guard. To inspect or edit it, either:

- Open it directly with 7-Zip (which recognises the ZIP signature regardless of extension).
- Rename it to `gamestate_common.zip` and open with any ZIP tool.

The same applies to difficulty-specific archives (e.g., `difficulty0_patched`, `difficulty1_patched`, etc.).

### Key XML Files Reference

Beyond the table in the [Game State XML Files](#game-state-xml-files) section, these files are particularly important for modding (source: filmboy84, skin36):

| File | Modding Use |
|---|---|
| `economy.xml` | Controls the market: item availability, base prices, stock levels, and weekly fluctuation. |
| `equipment_sets_by_level.xml` | Defines human tech loadouts per game progression level (what equipment organisations use as the game advances). |
| `equipment_sets_by_score.xml` | Defines alien loadouts per difficulty level. Found in the `difficulty*X*_patched` archives rather than in `common_patch`. |

### The modinfo.xml System (PR #725)

The mod system (introduced in PR #725) uses **additive patching**. When creating a mod, your XML files should only include the specific values you want to CHANGE. You do not need to reproduce the entire structure of the file you are patching. Unspecified fields retain their values from the previous layer.

### Image and Sound Overrides via datapath

A mod's `<datapath>` entry in `modinfo.xml` adds a directory to the virtual filesystem. Files placed here can override any game resource -- images, sounds, form definitions, etc. -- by mirroring the original ISO's directory structure. For example, to replace a weapon sprite, place your replacement image at the same relative path the game expects within your mod's data directory.

### SerializationTool for Delta Patches

The **SerializationTool** (in the `tools/` directory) can generate minimal delta patches between two game states. This is useful for creating mods that only contain the differences from a base state, rather than duplicating entire data files.

### Sound Format Support

OpenApoc supports the following sound formats for modding:

- **Raw PCM audio**: Referenced as `RAWSOUND:samplerate:path` (e.g., `RAWSOUND:22050:sounds/myeffect.raw`).
- **WAV**: Standard WAV files.
- **OGG Vorbis**: Compressed audio via libvorbis.

### Palette System

The game uses different palette systems in different contexts:

- **Cityscape**: Uses a 3-palette blend system that transitions between day, twilight, and night palettes based on the time of day.
- **Battlescape**: Uses a static palette. A dynamic palette system was planned but ultimately cut from the implementation.

Modders creating custom sprites should be aware of which palette context their assets will be used in.

### Armour Stat Mapping

When modding armour pieces, each armour slot maps to a specific agent stat bonus (source: Discord community):

| Armour Slot | Stat Affected |
|---|---|
| Legs | Speed |
| Arms | Accuracy |
| Helmet | Reactions |
| Chest | Bravery |

### Sprite Workflow and Asset Creation

Creating a single new weapon item is a significant undertaking. Community estimates (source: filmboy84) suggest approximately **12 hours of work**, of which only about 15 minutes is XML editing. The remaining time is spent on sprite creation. A complete weapon requires:

- **Equip screen icon** -- The inventory sprite shown in the equipment screen.
- **Dropped/thrown sprites** -- Sprites for the item when on the ground or in flight.
- **Shadow sprites** -- Corresponding shadow sprites for dropped/thrown states.
- **Handob sprites** -- The weapon as held by an agent, requiring sprites for each facing direction.
- **UFOpaedia image** -- The full-size reference image displayed in the in-game encyclopedia.

### Common Modding Pitfalls

The following issues are frequently encountered by new modders (source: Discord community, filmboy84, skin36):

- **CRC check errors**: If `Framework.Serialization.CRC` is enabled, manually editing `gamestate_common` or save files will invalidate the checksum. Disable CRC checking in `settings.cfg` when modding.
- **Case sensitivity in file paths**: Some platforms (especially Linux) are case-sensitive in file path resolution. Ensure your file references match the actual case exactly.
- **`op='delete'` deletes the WHOLE list**: The XML `op='delete'` attribute removes the entire list element, not just a single entry. There is currently no mechanism to delete individual entries from a list -- you can only replace the entire list.
- **Duplicate objects from serialization**: When creating new objects via mods, ensure unique keys. Duplicate keys can cause the serialization system to create duplicate entries with unpredictable behavior.

### Damage Type Limitations

Damage types are currently **hardcoded** in the engine. There is no modding capability for defining custom damage types. The available damage types are those defined in `damage_types.xml`, but their underlying behavior (penetration logic, resistance calculations, special effects like fire or stun) is implemented in C++ code.

### Extended Weapons Mod (EWM)

The **Extended Weapons Mod** by filmboy84 is currently the primary test platform for OpenApoc's modding system. It serves as both a playable content mod and a stress test for mod capabilities. Features include:

- Weapons ported from UFO: Enemy Unknown and Terror from the Deep.
- New alien types and variants.
- Over 2,000 additional agent names.
- Various balance adjustments and fixes.

The EWM is a useful reference for modders looking for real-world examples of what the mod system can accomplish and where its current limitations lie.

---

Sources:
- [`framework/modinfo.h`](https://github.com/OpenApoc/OpenApoc/blob/master/framework/modinfo.h)
- [`framework/luaframework.h`](https://github.com/OpenApoc/OpenApoc/blob/master/framework/luaframework.h)
- [`data/scripts/openapoc_base.lua`](https://github.com/OpenApoc/OpenApoc/blob/master/data/scripts/openapoc_base.lua)
- [`data/mods/base/modinfo.xml`](https://github.com/OpenApoc/OpenApoc/blob/master/data/mods/base/modinfo.xml)
- [`framework/options.cpp`](https://github.com/OpenApoc/OpenApoc/blob/master/framework/options.cpp)
