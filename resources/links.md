# External Resources

A curated collection of links related to OpenApoc, X-COM: Apocalypse, and the project's technical stack.

## UFOpaedia Wiki

The UFOpaedia is the primary community wiki for all X-COM games.

- [UFOpaedia Main Page](https://www.ufopaedia.org/index.php) -- encyclopaedia for all X-COM games
- [X-COM: Apocalypse](https://www.ufopaedia.org/index.php?title=Apocalypse) -- comprehensive reference for the original game, including mechanics, units, items, buildings, and strategies
- [OpenApoc](https://www.ufopaedia.org/index.php/OpenApoc) -- OpenApoc-specific documentation on the wiki
- [Differences to X-COM (OpenApoc)](https://www.ufopaedia.org/index.php?title=Differences_to_X-COM_(OpenApoc)) -- what OpenApoc changes or diverges from the original game
- [Known Bugs (Apocalypse)](https://www.ufopaedia.org/index.php?title=Known_Bugs_(Apocalypse)) -- documented bugs in the original X-COM: Apocalypse
- [Coding Style (OpenApoc)](https://www.ufopaedia.org/index.php/Coding_Style_(OpenApoc)) -- coding style guide on the wiki
- [Credits (OpenApoc)](https://www.ufopaedia.org/index.php/Credits_(OpenApoc)) -- project contributors

## GitHub

- [OpenApoc Repository](https://github.com/OpenApoc/OpenApoc) -- main source code repository
- [Issues](https://github.com/OpenApoc/OpenApoc/issues) -- bug tracker and feature requests
- [Pull Requests](https://github.com/OpenApoc/OpenApoc/pulls) -- code contributions under review
- [Releases](https://github.com/OpenApoc/OpenApoc/releases) -- prebuilt binaries and release notes
- [Wiki](https://github.com/OpenApoc/OpenApoc/wiki) -- GitHub wiki pages

### Milestone Issues

- [Playable Alpha](https://github.com/OpenApoc/OpenApoc/issues/263) -- tracking the alpha milestone
- [Beta](https://github.com/OpenApoc/OpenApoc/issues/264) -- tracking the beta milestone (all core features implemented)
- [Release 1.0](https://github.com/OpenApoc/OpenApoc/issues/265) -- tracking the 1.0 release milestone
- [Modding & Enhancements](https://github.com/OpenApoc/OpenApoc/issues/941) -- modding functions, extra features, and quality of life updates

### CI / Build Status

- [AppVeyor (Windows)](https://ci.appveyor.com/project/OpenApoc/openapoc/branch/master) -- Windows MSVC builds (also provides experimental build artifacts)

## Community

- [Discord](https://discord.gg/f8Rayre) -- the most active community hub for OpenApoc discussion, support, and development
- [Reddit (r/OpenApoc)](https://reddit.com/r/openapoc) -- subreddit for OpenApoc news and discussion
- [YouTube](https://www.youtube.com/c/OpenApoc) -- official YouTube channel with gameplay videos and development updates
- [Facebook](https://www.facebook.com/openapoc) -- community Facebook page
- [Transifex](https://www.transifex.com/x-com-apocalypse/apocalypse/) -- translation/localization platform for contributing translations

## Game Guides and References

- [StrategyWiki -- X-COM: Apocalypse](https://strategywiki.org/wiki/X-COM:_Apocalypse) -- strategy guide and walkthrough
- [GameFAQs -- X-COM: Apocalypse](https://gamefaqs.gamespot.com/pc/196880-x-com-apocalypse) -- community guides and FAQs
- [UFOpaedia -- Line of Sight](https://www.ufopaedia.org/index.php/Line_of_sight) -- technical reference for LOS mechanics
- [UFOpaedia -- Apocalypse Weapons](https://www.ufopaedia.org/index.php?title=Equipment_(Apocalypse)) -- weapon and equipment data
- [UFOpaedia -- Apocalypse Aliens](https://www.ufopaedia.org/index.php?title=Aliens_(Apocalypse)) -- alien species information

## Purchasing the Original Game

OpenApoc requires the original X-COM: Apocalypse game files. The game can be purchased from:

- [Steam -- X-COM: Apocalypse](https://store.steampowered.com/app/7660/XCOM_Apocalypse/)
- [GOG -- X-COM: Apocalypse](https://www.gog.com/game/xcom_apocalypse)

## Technical Documentation

Libraries and tools used by the OpenApoc project:

### Core Libraries

- [SDL2](https://www.libsdl.org) -- windowing, input, and audio
- [Boost](https://www.boost.org/) -- locale, program-options, UUID, CRC libraries
- [Qt6](https://www.qt.io/) -- launcher UI framework
- [libvorbis](https://xiph.org/vorbis/) -- OGG Vorbis audio decoding

### Bundled Libraries

- [fmtlib](https://fmt.dev/) -- string formatting library ([documentation](https://fmt.dev/latest/index.html))
- [GLM](https://glm.g-truc.net) -- OpenGL mathematics library
- [pugixml](https://pugixml.org) -- XML parsing and writing
- [PhysFS](https://icculus.org/physfs/) -- virtual filesystem abstraction
- [Lua](https://www.lua.org/) -- scripting language ([reference manual](https://www.lua.org/manual/5.4/))
- [miniz](https://github.com/richgel999/miniz) -- zlib-compatible compression
- [lodepng](https://github.com/lvandeve/lodepng) -- PNG image codec
- [magic_enum](https://github.com/Neargye/magic_enum) -- compile-time enum reflection
- [libsmacker](https://sourceforge.net/projects/libsmacker/) -- SMK video decoder

### Build and Development Tools

- [CMake](https://cmake.org/) -- build system generator ([documentation](https://cmake.org/documentation/))
- [Ninja](https://ninja-build.org/) -- build system
- [vcpkg](https://github.com/Microsoft/vcpkg) -- C++ package manager for Windows
- [clang-format](https://clang.llvm.org/docs/ClangFormat.html) -- automatic code formatting
- [clang-tidy](https://clang.llvm.org/extra/clang-tidy/) -- static analysis and linting
- [CTest](https://cmake.org/cmake/help/latest/manual/ctest.1.html) -- test runner

## See Also

- [Architecture](../development/architecture.md) -- OpenApoc codebase structure
- [Building](../development/building.md) -- build instructions for all platforms
- [Differences to X-COM](../comparison/differences.md) -- what OpenApoc changes from the original
