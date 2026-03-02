# Debug Mode and Cheat System

OpenApoc includes an extensive debug and cheat system not present in the original game. Debug hotkeys are toggled with **F1** in both the Cityscape and Battlescape. When enabled, various diagnostic and cheat functions become available.

> **Note:** The "Show debug commands on screen" option (`OpenApoc.NewFeature.DebugCommandsVisible`, default: true) in the More Options menu controls whether debug command buttons are visible in the UI.

---

## General Debug

Press **F1** to toggle debug mode on/off. When debug mode is active, some normal hotkeys are overridden by debug functions.

---

## Cityscape Debug

These hotkeys are available when debug mode is active (F1 toggled on) in the Cityscape view.

### Cheat Commands

| Key | Action |
|---|---|
| Ctrl + Alt + Shift + Left Click | Destroy scenery tile at cursor |
| Ctrl + Alt + Shift + Right Click | Collapse building at cursor |
| A | Give every vehicle weapon and ammo to current base |
| W | Warp to alien dimension and back |
| R | Repair all scenery in the city (instant, ignores repair rules) |
| Shift + R | Repair scenery using game repair logic (charges building owners, checks support) without requiring construction vehicles; single repair pass |
| B | Spawn UFO on base assault mission |
| U | Spawn three crashed UFOs |
| X | Crash every vehicle on map |
| - (Minus) | Destroy all currently selected vehicles (both owned and other) |
| P | Regenerate dimension gate portals in current city |
| PgUp / PgDown | Display only one map layer (other layers become transparent) |

### Diagnostic Overlays

| Key | Action |
|---|---|
| F2 | Show road pathfinding map |
| F3 | Highlight walk mode, collapsing tiles, basement tiles |
| F4 | Show aliens in buildings on strategy map |
| F5 | Show vehicle paths (blue = flying, yellow = ground) |
| F6 | Dump voxelmap for line of sight to `tileviewvoxels.png` |
| F7 | Dump voxelmap for line of sight to `tileviewvoxels.png` (fast mode, 1/4 of points) |
| F8 | Dump voxelmap for line of fire to `tileviewvoxels.png` |
| F9 | Dump voxelmap for line of fire to `tileviewvoxels.png` (fast mode, 1/4 of points) |
| F10 | Highlight tubes in city |
| F11 | Highlight roads in city |
| F12 | Highlight hills in city |
| T | Show vehicle target lines (green = X-COM targeting, red = other targeting, yellow = mutual targeting) |

### Numpad Filters

These filters work in conjunction with the F10/F11/F12 overlays to isolate specific map features:

| Key | Action |
|---|---|
| Numpad 1, 3, 7, 9 | Show only roads/tubes with an outgoing connection in that direction |
| Numpad 2 | Show only tubes with an outgoing connection downward |
| Numpad 8 | Show only tubes with an outgoing connection upward |
| Numpad 0 | Show all roads/tubes again (reset filter) |
| Numpad 5 | Toggle display mode (see details below) |

**Numpad 5 behavior by overlay type:**
- **Tubes (F10):** Switch between showing only tiles with defined tube passability, or also include tiles belonging to buildings
- **Roads (F11):** Switch between showing only tiles marked as "road", or also include tiles marked with road direction
- **Hills (F12):** Switch between showing only tiles marked as "road", or also include tiles marked with hill direction

---

## Battlescape Debug

These hotkeys are available when debug mode is active (F1 toggled on) in the Battlescape view.

### Unit Manipulation

| Key | Action |
|---|---|
| Middle Click | Activate teleportation mode for selected unit (regardless of whether it holds a charged teleporter) |
| E | Force end current turn in turn-based mode |
| R | Reveal whole map and show debug lines for which unit sees which unit |
| H | Restore stats of every unit, heal stun damage and fatal wounds |
| T | Restore TU of every player unit |

### Stun and Remove Commands

The **S** key stuns units and the **K** key removes units from the map (units count as retreated). Both support the same modifier combinations:

| Key Combination | Action |
|---|---|
| S | Stun unit under cursor |
| Ctrl + S | Stun units in small area around cursor |
| Shift + S | Stun everything **except** unit under cursor |
| Shift + Ctrl + S | Stun everything **except** units in small area around cursor |
| K | Remove unit under cursor from map |
| Ctrl + K | Remove units in small area around cursor |
| Shift + K | Remove everything **except** unit under cursor |
| Shift + Ctrl + K | Remove everything **except** units in small area around cursor |

### Morale and Psi

| Key | Action |
|---|---|
| P | Lower morale of every unit to trigger low morale events |
| Shift + P | Give every unit 0 psi defense and 100 psi energy/attack |

### Map Manipulation

| Key | Action |
|---|---|
| F | Re-link support lines for battlescape map parts |
| Q | Reset AI movement order for unit at selected tile (forces prone stance change) |
| Numpad 0 | Spawn vortex mine explosion at cursor |
| Numpad 1-9 | Spawn a high-damage shot at cursor in specified direction (5 = downward) |

### Voxel Dumps

| Key | Action |
|---|---|
| F6 | Dump voxelmap for line of sight to `tileviewvoxels.png` |
| F7 | Dump voxelmap for line of sight (fast mode, 1/4 of points) |
| F8 | Dump voxelmap for line of fire to `tileviewvoxels.png` |
| F9 | Dump voxelmap for line of fire (fast mode, 1/4 of points) |

---

## Base Screen Debug

| Context | Key | Action |
|---|---|---|
| Base View | F10 | Instantly finish all facility construction |
| Research Screen | F10 | Set research project to require only 100 more points (effectively completes the project at next update if at least 2 scientists are assigned) |

---

## Cheat Menu Options

In addition to debug hotkeys, OpenApoc provides a dedicated **Cheat Options** section accessible from the More Options menu. These are configurable via the `OpenApoc.Cheat` settings section.

### Multiplier Cheats

| Option | Config Key | Description | Type | Default |
|---|---|---|---|---|
| Infinite Ammo | `OpenApoc.Cheat.InfiniteAmmo` | Unlimited ammunition for all X-COM agents and vehicles | Boolean | false |
| Damage Inflicted Multiplier | `OpenApoc.Cheat.DamageInflictedMultiplier` | Multiplier for damage dealt by X-COM | Float | 1.0 |
| Damage Received Multiplier | `OpenApoc.Cheat.DamageReceivedMultiplier` | Multiplier for damage taken by X-COM | Float | 1.0 |
| Hostiles Multiplier | `OpenApoc.Cheat.HostilesMultiplier` | Multiplier for number of hostile units spawned | Float | 1.0 |
| Stat Growth Multiplier | `OpenApoc.Cheat.StatGrowthMultiplier` | Multiplier for agent stat growth rate | Float | 1.0 |

### Cheat Buttons

The cheat menu also provides quick-action buttons:

- **Give All Research** -- Instantly complete all research projects
- **Make All Organizations Friendly / Hostile** -- Set all organisation relationships to maximum positive or negative
- **Make All Organizations Utopia / Chaos** -- Push all organisation relations to extremes
- **Modify Funds** -- Add or set player funds
- **Go to End of Day** -- Advance clock to 23:59:59 of current day
- **Go Forward 1 Day** -- Skip exactly 1 day forward
- **Go Forward 1 Week** -- Skip exactly 7 days forward
- **Go to End of Week** -- Advance to last day of current week at 23:59:59
- **Go to End of Month** -- Advance to last day of current month at 23:59:59

---

## Tips

- Debug mode is toggled per-view: activating it in the Cityscape does not affect the Battlescape, and vice versa.
- When debug mode is active, some normal hotkeys (like S for Save in battlescape) are overridden by debug functions.
- The voxel dump commands (F6-F9) output an image file (`tileviewvoxels.png`) in the game's working directory. This is useful for diagnosing line-of-sight and line-of-fire issues.
- The `OpenApoc.NewFeature.DebugCommandsVisible` option controls whether debug buttons appear in the UI, but hotkeys work regardless when F1 debug mode is active.

---

Sources:
- [`README_HOTKEYS.txt`](https://github.com/OpenApoc/OpenApoc/blob/master/README_HOTKEYS.txt)
- [`framework/options.cpp`](https://github.com/OpenApoc/OpenApoc/blob/master/framework/options.cpp)
