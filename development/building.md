# Build Instructions

This page covers how to build OpenApoc from source on Windows, Linux, and macOS.

## Prerequisites

OpenApoc requires the original X-COM: Apocalypse game files to run. You will need a CD ISO image (or extracted directory) placed in the `data/` directory of the repository as `data/cd.iso`. GOG `.cue`/`.bin` files are also supported -- rename the `.cue` file to `cd.iso` and place both files in the `data/` folder.

### External Dependencies

The following libraries must be installed separately (via vcpkg on Windows, or system packages on Linux/macOS):

- [SDL2](https://www.libsdl.org) -- windowing, input, audio
- [Boost](https://boost.org) -- locale, program-options, uuid, crc libraries
- [Qt6](https://www.qt.io/) -- for the launcher (optional; disable with `BUILD_LAUNCHER=OFF`)
- [libvorbis](https://xiph.org/vorbis/) -- OGG Vorbis music decoding
- [libunwind](https://nongnu.org/libunwind/download.html) -- debug backtracing (Linux only)

### Bundled Dependencies (Git Submodules)

The following libraries are shipped as git submodules in the `dependencies/` directory and are built automatically. You do not need to install them separately:

- [GLM](https://glm.g-truc.net) -- math library
- [libsmacker](https://sourceforge.net/projects/libsmacker/) -- SMK video decoder
- [lodepng](https://github.com/lvandeve/lodepng) -- PNG reading/writing
- [Lua](https://www.lua.org/) -- scripting language
- [miniz](https://github.com/richgel999/miniz) -- zlib-compatible compression
- [PhysFS](https://icculus.org/physfs/) -- virtual filesystem for ISO reading (patched fork)
- [pugixml](https://pugixml.org) -- XML library
- [fmtlib](https://github.com/fmtlib/fmt) -- string formatting
- [magic_enum](https://github.com/Neargye/magic_enum) -- compile-time enum reflection

## Building on Windows

### Requirements

- [Visual Studio 2019 or later](https://visualstudio.microsoft.com/vs/) with the "Desktop Development with C++" workload
- A Git client (e.g., [GitHub Desktop](https://desktop.github.com/))
- [vcpkg](https://github.com/Microsoft/vcpkg) for dependency management

### Steps

1. **Clone the repository** and initialize submodules:

```cmd
git clone https://github.com/OpenApoc/OpenApoc.git
cd OpenApoc
git submodule update --init --recursive
```

2. **Install dependencies via vcpkg**:

For x64 builds:
```cmd
vcpkg --triplet x64-windows install sdl2 boost-locale boost-program-options boost-uuid boost-crc qt-base6-dev libvorbis
```

For x86 builds:
```cmd
vcpkg --triplet x86-windows install sdl2 boost-locale boost-program-options boost-uuid boost-crc qt-base6-dev libvorbis
```

Use `vcpkg help triplet` to list all supported architectures.

3. **Copy game files**: Place the original X-COM: Apocalypse `.iso` file into the `data/` directory as `cd.iso`.

4. **Open in Visual Studio**: Open the OpenApoc directory in Visual Studio. It should automatically detect and configure CMake. Set your configuration to x64-Release or x86-Release (must match your vcpkg triplet). Release is recommended since Debug builds are very slow.

5. **Configure vcpkg toolchain** (if not using vcpkg integration):

Visual Studio 2019+: Build > CMake Settings > Toolchain file > `<path to vcpkg>\scripts\buildsystems\vcpkg.cmake`

Or add to CMake settings JSON:
```json
"variables": [
    {
        "name": "CMAKE_TOOLCHAIN_FILE",
        "value": "<path to vcpkg>\\scripts\\buildsystems\\vcpkg.cmake"
    }
]
```

6. **Build**. The first build will take a while, especially if vcpkg is still installing dependencies. If you get errors, clear the CMake cache from the Project/CMake menu and try again.

7. **Run**: When running from within Visual Studio, the working directory is set to the repository root, so the `data/` folder is found automatically. To run outside Visual Studio, copy the entire `data/` folder (including `cd.iso`) into the directory containing `openapoc.exe`.

### Command-Line Build (Windows)

```cmd
cmake -B build -G Ninja -DCMAKE_TOOLCHAIN_FILE=<path to vcpkg>/scripts/buildsystems/vcpkg.cmake
cmake --build build
```

## Building on Linux

Tested on Ubuntu 22.04 and 24.04.

### Ubuntu

1. **Install dependencies**:

```sh
sudo apt-get install libsdl2-dev cmake build-essential git libunwind8-dev libboost-locale-dev libboost-program-options-dev qtbase5-dev libvorbis-dev
```

2. **Clone and initialize submodules**:

```sh
git clone https://github.com/OpenApoc/OpenApoc.git
cd OpenApoc
git submodule update --init --recursive
```

3. **Copy game files**:

```sh
cp /path/to/cd.iso data/
```

Note: The Steam version of X-COM: Apocalypse requires Steam Play to be enabled for installation on Linux.

4. **Configure and build**:

```sh
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo ..
make -j$(nproc)
```

5. **Run** (from the repository root):

```sh
./build/bin/OpenApoc
```

OpenApoc expects the `data/` folder to be in the current working directory.

### Fedora / Red Hat

```sh
sudo yum groupinstall "Development Tools" "Development Libraries"
sudo yum install git SDL2-devel cmake libunwind-devel qt6-qtbase-devel libvorbis-devel
```

Then follow the same clone, configure, and build steps as Ubuntu.

### Mageia

```sh
sudo urpmi "cmake(sdl2)" libstdc++-static-devel boost-devel boost unwind-devel task-c++-devel cmake git qt6-devel libvorbis-devel
```

Then follow the same clone, configure, and build steps as Ubuntu.

## Building on macOS

Tested on macOS Sequoia 15.6 (including Apple Silicon).

1. **Install Homebrew**:

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

2. **Clone and initialize submodules**:

```sh
git clone https://github.com/OpenApoc/OpenApoc.git
cd OpenApoc
git submodule update --init --recursive
```

3. **Install dependencies**:

```sh
brew install cmake boost pkg-config sdl2 qt@6 libvorbis
```

4. **Add Qt to your PATH**:

For zsh (macOS default since Catalina):
```sh
echo 'export PATH="/opt/homebrew/opt/qt@6/bin:$PATH"' >> ~/.zprofile
```

For bash:
```sh
echo 'export PATH="/opt/homebrew/opt/qt@6/bin:$PATH"' >> ~/.bashrc
```

Restart your shell or source the profile after this step.

5. **Copy game files**:

```sh
cp /path/to/cd.iso data/
```

6. **Configure and build**:

```sh
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo ..
make -j$(sysctl -n hw.ncpu)
```

7. **Run**:

```sh
cd ..
open ./build/bin/OpenApoc.app
```

## Build Options

Key CMake configuration options:

| Option | Description | Default |
|--------|-------------|---------|
| `CMAKE_BUILD_TYPE` | Build type (Debug, Release, RelWithDebInfo, MinSizeRel) | -- |
| `BUILD_LAUNCHER` | Build the Qt6 launcher application | ON |
| `CMAKE_TOOLCHAIN_FILE` | Path to vcpkg toolchain file (Windows) | -- |

## Running Tests

After building, run the test suite with CTest:

```sh
cd build
ctest
```

## Formatting and Linting

OpenApoc enforces code formatting with clang-format-18 and static analysis with clang-tidy-18.

Format all source files (from the build directory):
```sh
cmake --build build -t format-sources
```

Format specific files:
```sh
clang-format -i path/to/file.cpp path/to/file.h
```

Run static analysis:
```sh
cmake --build build -t tidy
```

Always run `clang-format -i` on modified files before committing. The CI lint check will reject unformatted code.

## System Requirements

- **Graphics**: OpenGL 2.0 capable video card (minimum). GLES 3.0 preferred.
- **Windows runtime**: Latest Visual C++ Redistributable ([download](https://docs.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist))
- **Disk space**: Approximately 1 GB for the build plus the original game files.

## Troubleshooting

- **CMake configuration fails**: Ensure all dependencies are installed and that vcpkg (on Windows) is using the correct triplet.
- **Submodule errors**: Run `git submodule update --init --recursive` to reset submodules to the correct versions. This will overwrite any changes in the `dependencies/` directory.
- **Missing cd.iso**: The extractors run during the build and require the original game data. Place `cd.iso` in `data/` before building.
- **Debug build too slow**: Use `RelWithDebInfo` instead of `Debug` for development. Debug builds have significantly reduced performance.

## See Also

- [Architecture](architecture.md) -- codebase structure overview
- [Coding Style](coding-style.md) -- formatting and naming conventions
- [OpenApoc Releases](https://github.com/OpenApoc/OpenApoc/releases) -- prebuilt binaries
