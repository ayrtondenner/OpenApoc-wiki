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

The UI widget system providing all interface controls.

- Controls, labels, text edits, listboxes, scrollbars, buttons, checkboxes, sliders, graphic elements.
- XML-based form definitions loaded from the `data/` directory.
- Widget hierarchy with parent-child relationships and layout management.

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

## See Also

- [Building](building.md) -- detailed build instructions for all platforms
- [Coding Style](coding-style.md) -- code formatting and naming conventions
- [Data Formats](data-formats.md) -- original game data format documentation
