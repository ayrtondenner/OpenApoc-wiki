# OpenApoc Wiki

Developer and game mechanics documentation for [OpenApoc](https://github.com/OpenApoc/OpenApoc), the open-source C++17 reimplementation of X-COM: Apocalypse (1997).

This repository is included as a git submodule in the main OpenApoc project under the `wiki/` directory.

## Contents

### Original Game Mechanics (`original-game/`)

Reference documentation for the original X-COM: Apocalypse mechanics, useful for developers implementing or verifying game systems.

- [Combat System](original-game/combat.md) — Real-time vs turn-based, damage types, weapons, armor, shields
- [Psionics](original-game/psionics.md) — Psi mechanics, stun, panic, mind control, psi-energy
- [City Management](original-game/city-management.md) — Mega-Primus, organizations, diplomacy, alien infiltration
- [Vehicles](original-game/vehicles.md) — Vehicle types, UFO types, aerial combat stats
- [Agents](original-game/agents.md) — Agent stats, training, types (human/hybrid/android)
- [Research & Manufacturing](original-game/research-manufacturing.md) — Tech tree, dual research branches
- [Base Building](original-game/base-building.md) — Facilities and base construction
- [Aliens](original-game/aliens.md) — Alien species, ecology, the alien dimension
- [Scoring & Difficulty](original-game/scoring-difficulty.md) — Score calculation, funding, dynamic difficulty
- [Known Bugs](original-game/known-bugs.md) — Documented bugs in the original game
- [Cut Features](original-game/cut-features.md) — Features planned but cut from the original

### OpenApoc Features (`openapoc/`)

Documentation specific to OpenApoc's additions and changes.

- [New Features](openapoc/new-features.md) — All 54+ configurable gameplay options
- [Controls](openapoc/controls.md) — Full control scheme with improved city controls
- [Modding](openapoc/modding.md) — XML data, Lua scripting, mod loading, save editing
- [Debug Mode](openapoc/debug-mode.md) — Debug hotkeys and cheat system
- [Notifications](openapoc/notifications.md) — 38 configurable pause notifications
- [Roadmap](openapoc/roadmap.md) — Development status and milestones

### Comparison (`comparison/`)

Side-by-side analysis of original vs OpenApoc.

- [Differences](comparison/differences.md) — Comprehensive list of differences
- [Bug Fixes](comparison/bug-fixes.md) — Original game bugs that OpenApoc fixes
- [Shared Mechanics](comparison/shared-mechanics.md) — Mechanics that work the same in both

### Development (`development/`)

Developer-focused documentation for contributing to OpenApoc.

- [Architecture](development/architecture.md) — High-level codebase architecture
- [Building](development/building.md) — Build instructions for all platforms
- [Data Formats](development/data-formats.md) — XML data format reference
- [Coding Style](development/coding-style.md) — Code style guide and conventions

### Research (`research/`)

Documentation of the AI-assisted research process that produced this wiki.

- [Research Statistics](research/research-stats.md) — Metrics and scale of the documentation overhaul
- [Discord Mining Summary](research/mining-summary.md) — 20 critical findings extracted from 77,612 Discord messages

### Resources (`resources/`)

- [Links](resources/links.md) — External references, community links, useful URLs

## How to Use

This wiki is included as a submodule in the OpenApoc repository:

```bash
# Clone OpenApoc with wiki:
git clone --recurse-submodules https://github.com/ayrtondenner/OpenApoc.git

# Or initialize after cloning:
git submodule update --init wiki

# Update wiki to latest:
cd wiki && git pull origin main && cd ..
git add wiki
git commit -m "Update wiki submodule"
```

## Contributing

Contributions are welcome! Please submit pull requests to this repository. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## External Wiki

Player-facing documentation is maintained on [UFOpaedia](https://www.ufopaedia.org/index.php/OpenApoc).

## License

GPL-3.0 — matching the OpenApoc project.
