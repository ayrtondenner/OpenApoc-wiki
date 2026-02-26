# Data Format Reference

OpenApoc extracts game data from the original X-COM: Apocalypse binary files and stores it in a human-readable XML format. This page documents the original binary data structures, the extraction process, and the resulting XML format.

## Overview

The original X-COM: Apocalypse stores its game data in packed binary structures within the executable (`UFO2P.EXE`) and various data files on the CD. OpenApoc includes extractor tools (`tools/extractors/`) that parse these binary formats and convert them into XML files that the engine reads at runtime.

The extraction process is:

```
Original CD ISO (data/cd.iso)
    |
    v  PhysFS reads the ISO
Binary data files (UFO2P.EXE, UFODATA/*, XCOM3/MAPS/*)
    |
    v  Extractor tools parse binary structures
OpenApoc XML game data (data/gamestate/*.xml)
```

## Original Binary Data Formats

The original game's data is documented in detail in the `tools/extractors/docs/` directory. The following sections summarize the key format specifications.

### Executable Data (UFO2P.EXE)

The main game executable contains most of the static game data embedded at fixed offsets. Each data type is stored as a packed array of fixed-size records.

#### Research Data

Each research topic is stored as a 28-byte record:

| Offset | Size | Field |
|--------|------|-------|
| 0 | 1 | Lab size required (0 = small, 1 = large) |
| 1 | 1 | Unknown (possibly related to prerequisite leads) |
| 2 | 1 | Unknown |
| 3 | 1 | Prerequisite type (0 = craft equip, 1 = agent equip, 3 = alien life form, FF = none) |
| 4 | 2 | Unknown |
| 6 | 2 | Prerequisite item index (FFFF = none) |
| 8 | 2 | Leads to research 1 (FFFF = none) |
| 10 | 2 | Leads to research 2 (FFFF = none) |
| 12 | 2 | Tech prerequisite 1 (FFFF = none) |
| 14 | 2 | Tech prerequisite 2 (FFFF = none) |
| 16 | 2 | Tech prerequisite 3 (FFFF = none) |
| 18 | 2 | Score value |
| 20 | 4 | Skill hours required |
| 24 | 1 | Research group (0 = biochemical, 1 = quantum physics) |
| 25 | 1 | UFOpaedia group (0-9, see below) |
| 26 | 2 | UFOpaedia entry index |

UFOpaedia groups: 0 = Vehicles, 1 = Base Facilities, 2 = Vehicle Equipment, 3 = Equipment, 4 = Organizations, 5 = VIPs, 6 = Aliens, 7 = Buildings, 8 = The Alien Dimension, 9 = Alien Craft.

#### Manufacturing Data

Each manufacturing topic is stored as a 48-byte record:

| Offset | Size | Field |
|--------|------|-------|
| 0 | 2 | Manufacturable (0 = false, 1 = true) |
| 2 | 4 | Skill hours required |
| 6 | 2 | Unused |
| 8 | 4 | Unused |
| 12 | 2 | Required research tech index |
| 14 | 2 | Unknown |
| 16-42 | 27 | Various unused/unknown fields |
| 42 | 4 | Manufacturing cost |
| 46 | 2 | Item type (0 = vehicle equip, 1 = agent equip, 2 = vehicle ammo, 3 = craft) |
| 48 | 2 | Item index |
| 50 | 2 | Lab size required (0 = small, 1 = large) |

#### Vehicle (Craft) Data

Each vehicle type is stored as a 126-byte record containing:

| Offset | Size | Field |
|--------|------|-------|
| 0 | 2 | Manufacturer (organization index) |
| 2 | 2 | Movement type (0 = ground, 1 = flying, 2 = overspawn) |
| 4 | 2 | Animation type (0 = UFO style, 1 = directional) |
| 6 | 6 | Size (x, y, z -- 2 bytes each) |
| 12 | 8 | Image positions (4 values, 2 bytes each) |
| 20 | 2 | Graphic frame index |
| 22 | 2 | Built-in acceleration |
| 24 | 2 | Built-in unknown |
| 26 | 2 | Built-in top speed |
| 28 | 8 | Shadow graphic data |
| 36 | 2 | Bullet fire position |
| 38 | 2 | Evasion chance (percentage) |
| 40 | 4 | Unknown/unused |
| 44 | 2 | Max constitution (hit points) |
| 46 | 2 | Downed HP threshold (for UFOs) |
| 48 | 2 | Weight |
| 50 | 12 | Armor values (rear, top, right, left, bottom, front -- 2 bytes each) |
| 62 | 2 | Passenger capacity |
| 64 | 2 | Aggressiveness (lower = more aggressive) |
| 66 | 2 | Score value |
| 68 | 1 | Equipment layout data file index |
| 69+ | -- | Equipment slot definitions and picture filename |

Note: All three values (acceleration, unknown, top speed) at offsets 22-26 must be non-zero to enable inter-dimensional travel. This does not work for ground vehicles.

#### Vehicle Equipment Data

Craft equipment is stored in 23-byte records:

| Offset | Size | Field |
|--------|------|-------|
| 0 | 1 | Item type (0 = engine, 1 = weapon, 2 = equipment) |
| 1 | 1 | Sub-data index |
| 2 | 2 | Item group (0 = ground only, 1 = air only, 2 = ammo, 3 = both) |
| 4 | 2 | Weight |
| 6 | 2 | Max ammo capacity |
| 8 | 2 | Ammo type used (FFFF = none) |
| 10 | 2 | Unknown |
| 12 | 2 | Picture index |
| 14 | 1 | Size X |
| 15 | 1 | Size Y |
| 16 | 4 | Unknown |
| 20 | 2 | Manufacturer |
| 22 | 2 | Buy limit |

#### Weapon Data

Craft weapon data is stored in 34-byte records:

| Offset | Size | Field |
|--------|------|-------|
| 0 | 2 | Projectile speed |
| 2 | 2 | Projectile image |
| 4 | 2 | Damage |
| 6 | 2 | Accuracy |
| 8 | 2 | Fire delay |
| 10 | 2 | Tail size |
| 12 | 2 | Guided (0 = false, 1 = true) |
| 14 | 2 | Turn rate (for guided weapons) |
| 16 | 2 | Range (value * 2) |
| 18 | 4 | Firing arc |
| 22 | 2 | Unknown |
| 24 | 2 | Point defence (0 = false, 1 = true) |
| 26 | 2 | Unknown |
| 28 | 2 | Firing sound index |
| 30 | 2 | Firing sound (duplicate?) |
| 32 | 2 | Explosion graphic (possibly damage type indicator) |

#### Building Data (CITYMAP5.BLD)

Each building record is 226 bytes:

| Offset | Size | Field |
|--------|------|-------|
| 0 | 2 | Building name index |
| 2 | 2 | X1 position |
| 4 | 2 | X2 position |
| 6 | 2 | Y1 position |
| 8 | 2 | Y2 position |
| 10 | 4 | Unknown |
| 14-167 | -- | Save game data (zeroed in base data) |
| 168 | 1 | Building function type |
| 169-217 | -- | Unknown fields |
| 218 | 1 | Purchasable flag |
| 219 | 1 | Owner (organization index) |

#### Known Data Locations in UFO2P.EXE (English)

| Offset Range | Content |
|-------------|---------|
| 1300148 - 1300691 | Facility data |
| 1302012 - 1303901 | UFO mission data |
| 1303904 - 1304463 | UFO crew data |
| 1304464 - 1305023 | UFO drop troops data |
| 1306240 - 1309011 | Research data |
| 1310004 - 1312152 | Manufacturing data |
| 1315942 - 1316442 | Funding data |
| 1349026 - 1349486 | Vehicle names |
| 1349488 - 1351087 | Agent equipment names |
| 1351122 - 1353322 | Building names |
| 1353324 - 1353639 | Facility names |
| 1353641 - 1354564 | Vehicle equipment names |
| 1355537 - 1355822 | Organization names |
| 1369018 - 1370656 | Research topics |
| 1370658 - 1376753 | Research descriptions |
| 1398132 - 1403112 | Unit stats data |
| 1612940 - 1617223 | Vehicle data |
| 1617224 - 1619550 | Vehicle equipment data |
| 1620416 - 1629103 | Vehicle slot data |
| 1681936 - 1682762 | Damage modifier data |
| 1682764 - 1689998 | Agent equipment data |

### Tactical Map Data (XCOM3/MAPS/)

Tactical maps are stored under `XCOM3/MAPS/` with each folder representing one tileset (a building or UFO type). Folder names contain a serial number and descriptive title (e.g., `07CORPHQ` for Corporate Headquarters, `58UFO8` for UFO Type 8).

#### BUILDING.DAT (1966 bytes)

| Offset | Size | Field |
|--------|------|-------|
| 0-11 | 12 | Chunk dimensions (x, y, z -- 4 bytes each) |
| 12-23 | 12 | Battlefield dimensions in chunks (x, y, z) |
| 24 | 1 | Allowed entrance directions (bitwise: N=bit0, E=bit1, S=bit2, W=bit3) |
| 25 | 1 | Allowed exit directions (same encoding) |
| 26-33 | 8 | Entrance level min/max (4 bytes each) |
| 34-41 | 8 | Exit level min/max (4 bytes each) |
| 42-1961 | 1920 | Exit locations (15 exits per side per level, up to 15 levels) |
| 1962-1965 | 4 | Destroyed ground tile index |

Exit locations are stored in groups of 16 four-byte values (the 16th is always `0xFFFFFFFF` as a terminator). The storage order is: right-wall exits for all levels first, then left-wall exits.

#### Section Files (XXSECYY.SDT, .SLS, .SMP, .SOB)

Each map section (a building block of the larger map) has up to four files:

**XXSECYY.SDT** (20 bytes): Section dimensions and occurrence limits.

| Offset | Size | Field |
|--------|------|-------|
| 0-11 | 12 | Chunk dimensions (x, y, z) |
| 12-15 | 4 | Minimum occurrences |
| 16-19 | 4 | Maximum occurrences |

**XXSECYY.SLS** (blocks of 136 bytes): Line of sight, waypoints, spawning, and AI priority data.

| Offset | Size | Field |
|--------|------|-------|
| 0-1 | 2 | Block validity flag (1 = valid) |
| 2-13 | 12 | Two 3D corner coordinates defining the block volume (inclusive) |
| 14-71 | 58 | Pathfinding/waypoint data (not fully decoded) |
| 72-129 | 58 | Sparse data fields |
| 130 | 1 | AI Patrol Priority (0-4) |
| 131 | 1 | AI Target Priority (0-4, always 0 in vanilla maps) |
| 132 | 1 | Spawn Type (0 = X-COM, 1 = Rival Organizations, 2 = Civilians) |
| 133 | 1 | Spawn Priority (0 = do not spawn, 1-4 = priority levels) |
| 134 | 1 | Can deploy large units (0 = no, 1 = yes) |
| 135 | 1 | Can deploy non-flying units (0 = no, 1 = yes) |

### Algorithms

The `tools/extractors/docs/algo.txt` file documents key algorithms used in the game, particularly:

#### Lazy Collision / Line of Sight

A tile-based collision algorithm that checks wall, ground, and feature visibility blocks as a ray passes through tiles. This "lazy" mode checks one sample per tile rather than per-voxel, trading accuracy for performance. The algorithm considers:

- Left wall blocks (when crossing tile boundaries in the X direction)
- Right wall blocks (when crossing tile boundaries in the Y direction)
- Ground blocks (when crossing tile boundaries in the Z direction)
- Feature blocks (objects within the tile)

#### Vision Algorithm

Based on the UFO: Enemy Unknown vision system. Key properties:

- 90-degree field of view cone based on unit facing direction.
- Maximum vision range of 20 tiles forward.
- Vision deteriorates at 1 tile forward per 2 tiles to the side.
- Smoke and fire accumulate vision blockage along the line of sight.
- Per-tile blockage is averaged over distance to prevent over/under-counting when rays cross tiles diagonally.

## OpenApoc XML Data Format

OpenApoc stores all game state as XML within ZIP archives. The XML format uses a key-value approach where game object properties are stored as nested elements.

### Save Game Structure

A save game (`.zip` file) contains multiple XML documents:

- **gamestate.xml** -- The root document containing all game state.
- Embedded references to other game objects use string IDs (e.g., `"ORG_MEGAPOL"`, `"VEHICLE_PHOENIX_HOVERCAR"`).

### Example XML Structure

Vehicle type definition (simplified):

```xml
<vehicletype id="VEHICLETYPE_PHOENIX_HOVERCAR">
    <name>Phoenix Hovercar</name>
    <manufacturer>ORG_SUPERDYNAMICS</manufacturer>
    <type>Flying</type>
    <health>100</health>
    <speed>14</speed>
    <acceleration>8</acceleration>
    <weight>1000</weight>
    <armour>
        <front>2</front>
        <rear>2</rear>
        <left>2</left>
        <right>2</right>
        <top>2</top>
        <bottom>2</bottom>
    </armour>
    <passengers>4</passengers>
    <score>50</score>
</vehicletype>
```

### Key XML Patterns

- **Object references**: Stored as string IDs that are resolved at load time via `StateRef<T>`.
- **Enumerations**: Stored as string names (using magic_enum for conversion).
- **Vectors**: Stored as space-separated coordinate values (e.g., `"1.0 2.5 3.0"` for a `Vec3<float>`).
- **Lists**: Stored as repeated child elements.
- **Boolean values**: Stored as `"true"` or `"false"` strings.

### Mod Data Format

Mods use the same XML format and can override or extend any game data. Mods are loaded from `data/mods/` (configurable) and are applied as overlays on the base game data.

## Data Reference Appendices

### Organization IDs

| Index | Organization |
|-------|-------------|
| 0x00 | X-COM |
| 0x01 | Alien |
| 0x02 | Government |
| 0x03 | Megapol |
| 0x04 | Cult of Sirius |
| 0x05 | Marsec |
| 0x06 | Superdynamics |
| 0x07 | General Metro |
| 0x08 | Cyberweb |
| 0x09 | Transtellar |
| 0x0A | Solmine |
| 0x0B | Sensovision |
| 0x0C | Lifetree |
| 0x0D | Nutrivend |
| 0x0E | Evonet |
| 0x0F | Sanctuary Clinic |
| 0x10 | Nanotech |
| 0x11 | Energen |
| 0x12 | Synthemesh |
| 0x13 | Gravball League |
| 0x14 | Psyke |
| 0x15 | Diablo |
| 0x16 | Osiron |
| 0x17 | S.E.L.F. |
| 0x18 | Mutant Alliance |
| 0x19 | Extropians |
| 0x1A | Technocrats |
| 0x1B | Civilian |

### Vehicle Type IDs

| Index | Vehicle |
|-------|---------|
| 0x00 | Alien Probe |
| 0x01 | Alien Scout |
| 0x02 | Alien Transporter |
| 0x03 | Alien Fast Attack Ship |
| 0x04 | Alien Destroyer |
| 0x05 | Alien Assault Ship |
| 0x06 | Alien Bomber |
| 0x07 | Alien Escort |
| 0x08 | Alien Battleship |
| 0x09 | Alien Mothership |
| 0x0A | Police Hovercar |
| 0x0B | Airtaxi |
| 0x0C | Rescue Transport |
| 0x0D | Construction Vehicle |
| 0x0E | Airtrans |
| 0x0F | Space Liner |
| 0x10 | Phoenix Hovercar |
| 0x11 | Hoverbike |
| 0x12 | Valkyrie Interceptor |
| 0x13 | Hawk Air Warrior |
| 0x14 | Dimension Probe |
| 0x15 | Biotrans |
| 0x16 | Explorer |
| 0x17 | Retaliator |
| 0x18 | Annihilator |
| 0x19 | Autotaxi |
| 0x1A | Autotrans |
| 0x1B | Police Car |
| 0x1C | Civilian Car |
| 0x1D | Stormdog |
| 0x1E | Wolfhound APC |
| 0x1F | Blazer Turbo Bike |
| 0x20 | Griffon AFV |
| 0x21 | Overspawn |

## Further Reading

- The full binary format documentation is in `tools/extractors/docs/` within the repository:
  - `hexa.txt` -- Comprehensive hex-level data format specifications
  - `tactical.txt` -- Tactical map file format details
  - `algo.txt` -- Algorithm documentation (collision, vision)
- [Architecture](architecture.md) -- how extractors fit into the build pipeline
- [X-COM: Apocalypse on UFOpaedia](https://www.ufopaedia.org/index.php?title=Apocalypse) -- community research on original game data
