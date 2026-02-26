# New Features and Configurable Options

OpenApoc extends the original X-COM: Apocalypse with a large number of configurable gameplay options. These are found in the **More Options** menu in-game and are stored in `settings.cfg`. Options are divided into categories: gameplay features added by OpenApoc (**OpenApoc.NewFeature**), mod-level balance changes (**OpenApoc.Mod**), and cheat/debug options (**OpenApoc.Cheat**).

All option names below correspond to keys in `settings.cfg` and can be set manually or through the in-game menus.

---

## Cityscape Options

These options affect city-level gameplay, vehicle behavior, and city management.

| Config Key | Description | Type | Default |
|---|---|---|---|
| `OpenApoc.NewFeature.OpenApocCityControls` | Improved city control scheme | Boolean | true |
| `OpenApoc.NewFeature.VanillaCityControls` | (Inverse of above) When disabled, vanilla city control scheme is used instead of the improved scheme | Boolean | true |
| `OpenApoc.NewFeature.FerryChecksRelationshipWhenBuying` | Transtellar checks relationship when buying items | Boolean | true |
| `OpenApoc.NewFeature.AllowManualCityTeleporters` | Allow manual use of teleporters in city | Boolean | true |
| `OpenApoc.NewFeature.AllowManualCargoFerry` | Allow manual ferrying of cargo and non-combatants | Boolean | true |
| `OpenApoc.NewFeature.AllowSoldierTaxiUse` | Allow soldiers to call taxi | Boolean | true |
| `OpenApoc.NewFeature.AllowAttackingOwnedVehicles` | Allow attacking owned vehicles | Boolean | true |
| `OpenApoc.NewFeature.CallExistingFerry` | Call existing transport instead of spawning them | Boolean | true |
| `OpenApoc.NewFeature.AlternateVehicleShieldSound` | Hitting vehicle shield produces alternate sound | Boolean | true |
| `OpenApoc.NewFeature.StoreDroppedEquipment` | Attempt to recover agent equipment dropped in city | Boolean | true |
| `OpenApoc.NewFeature.CrashingGroundVehicles` | Unsupported ground vehicles crash (Weapons and Modules may be lost in crash) | Boolean | true |
| `OpenApoc.NewFeature.EnforceCargoLimits` | Enforce vehicle cargo limits | Boolean | false |
| `OpenApoc.NewFeature.AllowNearbyVehicleLootPickup` | Allow nearby vehicles to pick up loot | Boolean | true |
| `OpenApoc.NewFeature.AllowBuildingLootDeposit` | Allow loot to be stashed in the building | Boolean | true |
| `OpenApoc.NewFeature.ArmoredRoads` | Armored roads | Boolean | true |
| `OpenApoc.NewFeature.CollapseRaidedBuilding` | Successful raid collapses building | Boolean | false |
| `OpenApoc.NewFeature.ScrambleOnUnintentionalHit` | Any hit on hostile building provokes retaliation | Boolean | false |
| `OpenApoc.NewFeature.MarketOnRight` | Put market stock on the right side | Boolean | true |
| `OpenApoc.NewFeature.CrashingDimensionGate` | Incapable vehicles crash when entering gates (Weapons and Modules may be lost in crash) | Boolean | true |
| `OpenApoc.NewFeature.CrashingOutOfFuel` | Vehicles crash when out of fuel (Weapons and Modules may be lost in crash) | Boolean | true |
| `OpenApoc.NewFeature.SkipTurboMovement` | Skip turbo movement calculations | Boolean | false |
| `OpenApoc.NewFeature.ATVUFOMission` | Allow All Terrain Vehicles (ATV) to initiate UFO recovery missions | Boolean | true |
| `OpenApoc.NewFeature.ShowCurrentDimensionVehicles` | Show vehicles in current dimension (or entering / leaving) | Boolean | true |
| `OpenApoc.NewFeature.ShowNonXCOMVehiclesPrefix` | Add prefix to non-X-COM vehicles | Boolean | true |
| `OpenApoc.NewFeature.IsoOnlyFollow` | Don't follow vehicles in strategy view | Boolean | false |

---

## Battlescape Options

These options affect tactical battle gameplay, unit behavior, and combat mechanics.

| Config Key | Description | Type | Default |
|---|---|---|---|
| `OpenApoc.NewFeature.UFODamageModel` | X-Com 1 Damage model (0-200%) | Boolean | false |
| `OpenApoc.NewFeature.InstantExplosionDamage` | Explosions damage instantly | Boolean | true |
| `OpenApoc.NewFeature.GravliftSounds` | Gravlift sounds | Boolean | true |
| `OpenApoc.NewFeature.NoInstantThrows` | Throwing requires proper facing and pose | Boolean | true |
| `OpenApoc.NewFeature.PayloadExplosion` | Ammunition explodes when blown up | Boolean | true |
| `OpenApoc.NewFeature.DisplayUnitPaths` | Display unit paths in battle | Boolean | true |
| `OpenApoc.NewFeature.AdditionalUnitIcons` | Display additional unit icons (fatal, psi) | Boolean | true |
| `OpenApoc.NewFeature.AllowForceFiringParallel` | Allow force-firing parallel to the ground | Boolean | true |
| `OpenApoc.NewFeature.RequireLOSToMaintainPsi` | Require LOS to maintain psi attack | Boolean | false |
| `OpenApoc.NewFeature.RunAndKneel` | All units run and kneel by default | Boolean | true |
| `OpenApoc.NewFeature.AutoReload` | Automatically reload weapons when empty | Boolean | true |
| `OpenApoc.NewFeature.LoadSameAmmo` | Weapons autoreload only same ammo type | Boolean | true |
| `OpenApoc.NewFeature.BattlescapeVertScroll` | Mousewheel changes vertical level in battlescape | Boolean | true |

---

## General / UI Options

These options affect interface behavior, controls, and general game settings.

| Config Key | Description | Type | Default |
|---|---|---|---|
| `OpenApoc.NewFeature.DebugCommandsVisible` | Show the debug commands on screen | Boolean | true |
| `OpenApoc.NewFeature.NoScrollSounds` | Disable scrolling sounds | Boolean | false |
| `OpenApoc.NewFeature.AdvancedInventoryControls` | Allow unloading clips and quick equip | Boolean | true |
| `OpenApoc.NewFeature.EnableAgentTemplates` | Enable agent equipment templates | Boolean | true |
| `OpenApoc.NewFeature.SeedRng` | Seed RNG on game start | Boolean | true |
| `OpenApoc.NewFeature.LeftClickIconEquip` | Left clicking icon opens equip menu | Boolean | false |
| `OpenApoc.NewFeature.SingleSquadSelect` | Select squad with single click | Boolean | false |
| `OpenApoc.NewFeature.formatAsCurrency` | Use currency formatting | Boolean | true |
| `Options.Misc.AutoScroll` | Enable scrolling with mouse | Boolean | true |
| `Options.Misc.ActionMusic` | Music changes according to action in battle | Boolean | true |
| `Options.Misc.AutoExecute` | Execute remaining orders when player presses end turn button | Boolean | false |
| `Options.Misc.ToolTipDelay` | Delay in milliseconds before showing tooltips (<= 0 to disable) | Integer | 500 |
| `Options.Misc.VanillaToggle` | Toggle vanilla mode | Boolean | false |

---

## Mod Options

These options are gameplay balance changes that behave like lightweight mods. They are found in the `OpenApoc.Mod` section and can meaningfully alter game balance.

| Config Key | Description | Type | Default |
|---|---|---|---|
| `OpenApoc.Mod.MaxTileRepair` | Construction Vehicles will repair a maximum of X tiles per night | Integer | 5 |
| `OpenApoc.Mod.SceneryRepairCostFactor` | Percentage of the original price organisations must pay for scenery tile repairs | Float | 10.0 |
| `OpenApoc.Mod.StunHostileAction` | Stunning hurts relationships | Boolean | false |
| `OpenApoc.Mod.RaidHostileAction` | Initiating raid hurts relationships | Boolean | false |
| `OpenApoc.Mod.BSKLauncherSound` | (MOD) Original Brainsucker Launcher SFX | Boolean | true |
| `OpenApoc.Mod.InvulnerableRoads` | (MOD) Invulnerable roads | Boolean | false |
| `OpenApoc.Mod.ATVTank` | (MOD) Griffon becomes All-Terrain | Boolean | true |
| `OpenApoc.Mod.ATVAPC` | (MOD) Wolfhound APC becomes All-Terrain | Boolean | true |
| `OpenApoc.Mod.CrashingVehicles` | Vehicles crash on low HP (Weapons and Modules may be lost in crash) | Boolean | false |
| `OpenApoc.Mod.ScriptsList` | Semicolon-separated list of scripts to load | String | `scripts/openapoc_base.lua;` |

---

## Cheat Options

These options are found in the `OpenApoc.Cheat` section and provide difficulty adjustment or outright cheating capabilities.

| Config Key | Description | Type | Default |
|---|---|---|---|
| `OpenApoc.Cheat.InfiniteAmmo` | Infinite ammo for X-Com agents and vehicles | Boolean | false |
| `OpenApoc.Cheat.DamageInflictedMultiplier` | Multiplier for damage inflicted by X-Com | Float | 1.0 |
| `OpenApoc.Cheat.DamageReceivedMultiplier` | Multiplier for damage received by X-Com | Float | 1.0 |
| `OpenApoc.Cheat.HostilesMultiplier` | Multiplier for number of hostiles | Float | 1.0 |
| `OpenApoc.Cheat.StatGrowthMultiplier` | Multiplier for agent stat growth | Float | 1.0 |

---

## Framework and Engine Options

These are lower-level settings controlling the engine, display, audio, and data management.

### Display

| Config Key | Description | Type | Default |
|---|---|---|---|
| `Framework.Screen.Width` | Initial screen width (in pixels) | Integer | 1280 |
| `Framework.Screen.Height` | Initial screen height (in pixels) | Integer | 720 |
| `Framework.Screen.Fullscreen` | Deprecated: use ScreenMode instead | Boolean | false |
| `Framework.Screen.Mode` | Mode: windowed, fullscreen, or borderless | String | `windowed` |
| `Framework.Screen.Display` | Display number in multi-monitor setup (0..n) | Integer | 0 |
| `Framework.Screen.ScaleX` | Scale screen in X direction by (percent) | Integer | 100 |
| `Framework.Screen.ScaleY` | Scale screen in Y direction by (percent) | Integer | 100 |
| `Framework.Screen.AutoScale` | Automatically scale up game viewport for modern screens (overrides ScaleX and ScaleY) | Boolean | false |

### Audio

| Config Key | Description | Type | Default |
|---|---|---|---|
| `Framework.Audio.GlobalGain` | Global audio gain (0-20) | Integer | 20 |
| `Framework.Audio.SampleGain` | Sample audio gain (0-20) | Integer | 20 |
| `Framework.Audio.MusicGain` | Music audio gain (0-20) | Integer | 20 |
| `Framework.Audio.ConcurrentSamples` | The number of concurrent samples to play at one time | Integer | 10 |

### Engine

| Config Key | Description | Type | Default |
|---|---|---|---|
| `Framework.Data` | The path containing OpenApoc data | String | `./data` |
| `Framework.CD` | The path to the XCom:Apocalypse CD | String | `./data/cd.iso` |
| `Framework.ThreadPoolSize` | Number of threads for the threadpool (0 = auto-detect) | Integer | 0 |
| `Framework.Renderers` | ':' separated list of renderer backends (in preference order) | String | `GLES_3_0:GL_2_0` |
| `Framework.AudioBackends` | ':' separated list of audio backends (in preference order) | String | `SDLRaw:null` |
| `Framework.Language` | The language used in-game (empty for system default) | String | (empty) |
| `Framework.MouseCapture` | Enable mouse capture for the window | Boolean | false |
| `Framework.TargetFPS` | The target FPS count (affects game speed) | Integer | 60 |
| `Framework.FrameLimit` | Quit after this many frames (0 = unlimited) | Integer | 0 |
| `Framework.SwapInterval` | Swap interval (0 = tear, 1 = wait for vsync) | Integer | 0 |
| `Framework.EnableTouchEvents` | Enable touch events | Boolean | false |

### Data Cache

| Config Key | Description | Type | Default |
|---|---|---|---|
| `Framework.Data.ImageCacheSize` | Number of Images to keep in data cache | Integer | 100 |
| `Framework.Data.ImageSetCacheSize` | Number of ImageSets to keep in data cache | Integer | 10 |
| `Framework.Data.VoxelCacheSize` | Number of VoxelMaps to keep in data cache | Integer | 1 |
| `Framework.Data.FontStringCacheSize` | Number of rendered font strings to keep in data cache | Integer | 100 |
| `Framework.Data.PaletteCacheSize` | Number of Palettes to keep in data cache | Integer | 10 |

### Logging

| Config Key | Description | Type | Default |
|---|---|---|---|
| `Logger.FileLevel` | Loglevel to output to file (0 = nothing, 1 = error, 2 = warning, 3 = info, 4 = debug) | Integer | 3 |
| `Logger.BacktraceLevel` | Loglevel to print a backtrace to file log (0 = nothing, 1 = error, 2 = warning, 3 = info, 4 = debug) | Integer | 1 |
| `Logger.dialogLevel` | Loglevel to pop up a dialog (0 = nothing, 1 = error, 2 = warning, 3 = info, 4 = debug) | Integer | 1 |

### Serialization

| Config Key | Description | Type | Default |
|---|---|---|---|
| `Framework.Serialization.CRC` | Use a CRC checksum when saving files | Boolean | false |
| `Framework.Serialization.SHA1` | Use a SHA1 checksum when saving files | Boolean | false |

### Save Games

| Config Key | Description | Type | Default |
|---|---|---|---|
| `Game.Save.Directory` | Directory containing saved games | String | `./saves` |
| `Game.Save.Pack` | Pack saved games into a zip | Boolean | true |

### Game Loading

| Config Key | Description | Type | Default |
|---|---|---|---|
| `Game.SkipIntro` | Skip intro video | Boolean | false |
| `Game.Load` | Path to save game to load at startup | String | (empty) |
| `Game.Mods` | A colon-separated list of mods to load (relative to mod directory) | String | `base` |
| `Game.ModPath` | Directory containing mods | String | `./data/mods` |
| `Game.ASyncLoading` | Load in background while displaying animated loading screen | Boolean | true |

### Miscellaneous

| Config Key | Description | Type | Default |
|---|---|---|---|
| `Forms.TooltipFont` | The default tooltip font | String | `smallset` |
| `Trace.enable` | Enable json call/time tracking | Boolean | false |
| `Trace.outputFile` | File to output trace json to | String | `openapoc.trace` |

---

## Notes

- Options under `OpenApoc.NewFeature` represent gameplay additions and quality-of-life improvements introduced by OpenApoc that are not present in the original game.
- Options under `OpenApoc.Mod` are balance-affecting changes that are applied at runtime through the Lua scripting system (via the `applyMods` hook), so they can be changed between sessions without starting a new game.
- Options under `OpenApoc.Cheat` are intended for testing or casual play and can trivialize the game if set to extreme values.
- All options can be edited directly in `settings.cfg` or changed through the in-game menus.

Source: [`framework/options.cpp`](https://github.com/OpenApoc/OpenApoc/blob/master/framework/options.cpp)
