# Codebase Architecture

This page describes the high-level architecture of the OpenApoc codebase. OpenApoc is written in C++17 and built with CMake (minimum 3.30) using the Ninja generator. It targets GCC 8+, Clang 7+, and MSVC 2019+.

## Directory Structure

```
OpenApoc/
  library/        Core utilities
  framework/      Engine core
  forms/          UI widget system
  game/state/     Game logic and state
  game/ui/        Game UI screens
  tools/          Extractors, editor, launcher
  tests/          CTest unit tests
  dependencies/   Git submodules (bundled libraries)
  data/           Game data, XML forms, fonts, language files, mods
```

### library/

Core utility types and functions used throughout the entire codebase.

- **`strings.h`** -- `UString`, the project's standard string type. All strings in OpenApoc are `UString`. All `char*` and `std::string` values are assumed to be UTF-8.
- **`sp.h`** -- Smart pointer type aliases:
  - `sp<T>` -- `std::shared_ptr<T>`
  - `up<T>` -- `std::unique_ptr<T>`
  - `wp<T>` -- `std::weak_ptr<T>`
  - `mksp<T>(args...)` -- `std::make_shared<T>(args...)`
  - `mkup<T>(args...)` -- `std::make_unique<T>(args...)`
- **`colour.h`** -- `Colour` type for RGBA color representation.
- **`vec.h`** -- `Vec2<T>` and `Vec3<T>` template vector types for 2D and 3D coordinates.
- **`strings_format.h`** -- `OpenApoc::format()` function wrapping fmtlib for string formatting with `{0}`, `{1}`, etc. positional placeholders.
- **`rect.h`** -- `Rect<T>` template for axis-aligned rectangles.

### framework/

The engine core that provides platform abstraction and essential services.

- **Rendering**: Supports GLES 3.0 (preferred) and GL 2.0 (fallback). The renderer abstraction allows different backends.
- **Sound**: Audio playback via SDL2 with libvorbis for OGG music decoding. Separate volume controls for music and sound effects.
- **Filesystem**: Uses a patched version of PhysFS to read data from the original game's CD ISO image and from directory trees. This patched PhysFS is critical -- it enables reading `.iso` files directly.
- **Events**: Event system for input handling (keyboard, mouse) and game events.
- **Logging** (`logger.h`): Logging macros using fmt-style format strings:
  - `LogInfo("message {0}", arg)` -- general information
  - `LogWarning("message {0}", arg)` -- recoverable errors
  - `LogError("message {0}", arg)` -- fatal errors
- **Serialization**: XML-based serialization using pugixml, with game states stored as XML inside ZIP archives (using miniz for compression).
- **Configuration**: Settings management via Boost.ProgramOptions.
- **Localization**: Translation support via Boost.Locale and the `tr()` function.

### forms/

The UI widget system providing all interface controls. Forms are defined in XML files (`data/forms/`) and loaded at runtime via pugixml.

- 14 control types: Form, Label, TextButton, GraphicButton, Graphic, CheckBox, RadioButton, TriStateBox, ScrollBar, ListBox, MultilistBox, TextEdit, Ticker, plus the base Control class.
- Hierarchical parent-child control tree with event callbacks.
- XML-based layout with support for centering, percentage sizing, and palette-based rendering.

See [Forms UI](forms-ui.md) for the complete reference.

### game/state/

All game logic and state management, organized into subdirectories:

- **`city/`** -- Cityscape logic: buildings, vehicles, vehicle missions, city map, projectiles, scenery, organizations.
- **`battle/`** -- Tactical combat: battle map, battle units, AI, items, projectiles, movement, line of sight.
- **`rules/`** -- Game rule definitions: damage types, facility types, vehicle types, agent types, equipment definitions.
- **`GameState`** -- The central class holding all game state. This is the root object for serialization.
- **`StateRef<T>`** -- A serialization-aware reference type that stores an ID string and lazily resolves to the actual object. This is how cross-references between game objects survive save/load cycles.

### game/ui/

Game UI screens organized by game phase:

- **City view**: Main cityscape display, organization screens, base management, vehicle and agent management, market/transaction screens.
- **Battle view**: Tactical combat display, unit selection, action panels.
- **UFOpaedia**: In-game encyclopedia screens.
- **Base management**: Facility placement, research/manufacturing assignment, agent equipment.
- **General**: Main menu, options, save/load, skirmish mode setup.

### tools/

Utility programs and scripts:

- **Extractors** (`tools/extractors/`): Read the original game's binary data files from the CD ISO and convert them into OpenApoc's XML format. This is run during the build process.
- **Editor**: A map/data editor tool.
- **Launcher**: A Qt6-based graphical launcher for configuring and starting the game. Can be disabled with the `BUILD_LAUNCHER` CMake option.
- **Code generators**: Scripts for generating boilerplate code.
- **Lint scripts**: Formatting and static analysis helpers.

### tests/

Unit tests run via CTest. Tests cover core library functions, serialization, and selected game logic.

### dependencies/

Nine bundled git submodules that are built directly as part of the project:

| Library | Purpose |
|---------|---------|
| [fmt](https://github.com/fmtlib/fmt) | String formatting (C++20 std::format predecessor) |
| [GLM](https://glm.g-truc.net) | Mathematics library (vectors, matrices) |
| [lodepng](https://github.com/lvandeve/lodepng) | PNG image reading/writing |
| [Lua](https://www.lua.org/) | Scripting language for modding |
| [magic_enum](https://github.com/Neargye/magic_enum) | Compile-time enum reflection |
| [miniz](https://github.com/richgel999/miniz) | Zlib-compatible compression (ZIP archives) |
| [PhysFS](https://icculus.org/physfs/) | Virtual filesystem for ISO/directory access (patched fork) |
| [pugixml](https://pugixml.org) | XML parsing and writing |
| [libsmacker](https://sourceforge.net/projects/libsmacker/) | SMK video file decoder |

### data/

Runtime data including:

- XML form definitions for all UI screens.
- Font files.
- Language/translation files.
- Mod data directory (`data/mods/`).
- The original game's CD ISO (`data/cd.iso`) must be placed here by the user.

## Key Architectural Patterns

### StateRef\<T\> -- Serializable References

`StateRef<T>` is fundamental to how OpenApoc manages cross-references between game objects. Instead of raw pointers or smart pointers, game objects reference each other through `StateRef` which stores:

1. A string ID (the serialized form).
2. A lazy-resolved pointer to the actual object (looked up from `GameState`).

This enables:
- Clean XML serialization (references become string IDs).
- Safe save/load cycles without pointer fixup.
- Human-readable save files where relationships between objects are visible.

### GameState -- Central State Container

`GameState` is the single root object that owns all game state. It contains maps of all game objects indexed by their string IDs. When a save game is loaded, `GameState` is populated from XML, and all `StateRef` instances resolve their pointers through it.

### XML Serialization Pipeline

```
Game State (C++ objects)
    |
    v  serialize
XML documents (pugixml DOM trees)
    |
    v  compress
ZIP archive (miniz)  -->  .zip save file on disk
```

Loading reverses this pipeline: ZIP is decompressed, XML is parsed, and C++ game objects are constructed from the XML data.

### Original Data Extraction

```
Original CD ISO (data/cd.iso)
    |
    v  PhysFS (patched)
Binary data files (UFO2P.EXE, UFODATA/*, XCOM3/*)
    |
    v  Extractor tools (tools/extractors/)
OpenApoc XML game data (data/gamestate/*.xml)
```

The extractors run during the build process to convert the original game's proprietary binary formats into OpenApoc's XML format. This extracted data provides all game rules, stats, maps, and content definitions.

### Rendering Pipeline

OpenApoc supports two rendering backends:

- **GLES 3.0** (preferred): Used on most modern systems. Provides better performance and shader support.
- **GL 2.0** (fallback): For older hardware compatibility.

The renderer is abstracted behind a common interface, so game code does not interact with OpenGL directly. The game runs at 60 FPS with support for arbitrary screen resolutions and display scaling.

## Build System

CMake (minimum 3.30) with the Ninja generator. Key CMake options:

- `CMAKE_TOOLCHAIN_FILE` -- Path to vcpkg toolchain (Windows).
- `CMAKE_BUILD_TYPE` -- `RelWithDebInfo` recommended for development.
- `BUILD_LAUNCHER` -- Enable/disable the Qt6 launcher (default ON).

External dependencies (installed separately or via vcpkg):
- SDL2, Boost (locale, program-options, uuid, crc), Qt6, libvorbis, libunwind (Linux only).

## Community Architecture Insights

The following insights come from OpenApoc Discord discussions with core developers and contributors. They provide additional context on architectural decisions, known design flaws, and implementation details not captured in the code comments.

### StateRef/StateObject System -- Known Design Flaw

The `StateRef<T>` / `StateObject` system, while functional, is acknowledged by lead developer JonnyH as a significant architectural problem. In his words, it is **"a mess of pointers and weird shared ownership."** This system is the **root cause of all "Missing Object" errors** that players encounter -- these occur when a `StateRef` holds an ID string that no longer resolves to a valid object in `GameState`.

JonnyH has stated that if starting the project from scratch today, he would use an **Entity Component System (ECS)** architecture instead. ECS would provide cleaner ownership semantics, better cache locality, and simpler serialization. However, migrating the existing codebase to ECS would be an enormous undertaking and is not planned. Instead, the current approach is an incremental `StateRef<>` rework (ongoing as of 2025) to address the worst failure modes.

### State/UI Separation Constraint

There is a strict architectural boundary between `game/state/` and `game/ui/`: **game state code cannot call into game UI code directly**. Attempting to do so causes linker errors because the two are compiled as separate libraries with a one-way dependency (UI depends on state, but not vice versa).

This means that game logic in `game/state/` cannot trigger UI updates, display messages, or manipulate the interface. All communication from state to UI must flow through the event system or through data that the UI polls during its render/update cycle.

### Serialization System

The serialization system has several notable characteristics (source: JonnyH, Discord):

- **Code-generated**: Serialization code is generated from `gamestate_serialize.xml` at build time. This XML file defines the mapping between C++ game state objects and their XML representations.
- **High memory usage**: The generated serialization file requires **3GB+ of RAM** to compile. This is a known pain point for developers with limited system memory.
- **Save game format**: Save games are ZIP archives containing XML files (using miniz for compression and pugixml for XML handling).

### Game State Layered Loading

The game state loading pipeline works as follows:

```
gamestate_common (base extracted data)
    |
    v  merge
common_patch (OpenApoc corrections and additions)
    |
    v  merge
difficulty*N*_patch (difficulty-specific overrides)
    |
    v  merge
mod patches (in Game.Mods order)
```

Each layer can add new objects or override individual fields of existing objects. The merge is additive -- fields not mentioned in a patch retain their values from the previous layer.

### No Initial Design Document

According to community discussion, the project **had no formal design document** at its inception. JonnyH has noted that "there wasn't any design -- the initial stuff was done concurrently with people documenting the OG behavior." This organic development approach explains some of the architectural inconsistencies in the codebase, such as the mixed TPS assumptions and the `StateRef` design.

### STL Container Iteration Safety

A recurring source of bugs in the codebase is **modifying STL containers while iterating over them**. This pattern causes undefined behavior in C++ and has led to crashes and data corruption bugs. The established solution in OpenApoc is to:

1. Iterate the container and **mark items for deletion** (e.g., using a flag or a separate list of keys to remove).
2. After the iteration completes, perform the actual deletions.

This "mark and sweep" pattern must be followed whenever game logic needs to remove items from a container during an update tick.

### Voxel System

The voxel collision system used for line-of-sight and projectile hit detection has the following characteristics:

- **LOFTemps** (Line of Fire Templates): Operate at **32x32x32** or **64x64x64** resolution depending on the tile type.
- **Single ray**: Hit detection casts a single ray from the firing position to the target voxel. This can produce degenerate cases where shots miss targets they visually appear to hit, or vice versa.
- **Performance**: The voxel system is computationally expensive. GCC Profile-Guided Optimization (PGO) provides approximately a **5x speedup** for voxel-heavy operations like batch line-of-sight calculations.

### Original Game Two-Executable Architecture

The original X-COM: Apocalypse used a **two-executable architecture**:

- **`ufop.exe`**: The cityscape executable, handling city management, vehicle combat, base management, and strategic layer.
- **`tacp.exe`**: The battlescape (tactical) executable, handling ground combat missions.

The two executables exchanged data via intermediate files on disk. When a tactical mission was initiated from the cityscape, `ufop.exe` wrote the mission parameters to disk, launched `tacp.exe`, and then read the results back when tactical combat concluded.

OpenApoc unifies both game phases into a single executable, which simplifies data exchange but also means the codebase must manage both city and battle states simultaneously.

---

## See Also

- [Building](building.md) -- detailed build instructions for all platforms
- [Coding Style](coding-style.md) -- code formatting and naming conventions
- [Data Formats](data-formats.md) -- original game data format documentation
