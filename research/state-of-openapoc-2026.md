# State of OpenApoc — February 2026

A comprehensive assessment of the OpenApoc project compiled from codebase analysis, GitHub activity, UFOpaedia documentation, and 77,612 Discord messages spanning 8+ years of community discussion.

## Project Overview

OpenApoc is an open-source C++17 reimplementation of X-COM: Apocalypse (1997), licensed under GPL-3.0. The project aims to faithfully recreate the original game while adding modern improvements and eventually restoring cut features from the beta versions.

- **Repository**: [OpenApoc/OpenApoc](https://github.com/OpenApoc/OpenApoc)
- **Stars**: ~564
- **License**: GPL-3.0
- **Lead Developer**: JonnyH (engine, rendering, backend)
- **Key Contributors**: filmboy84 (testing, modding, OG knowledge), skin36 (reverse engineering), Kurtsley (bug fixes, relations system)

## Current State: Alpha

**OpenApoc is playable from start to finish**, but it is **not feature complete**. As confirmed by multiple community testers (2024-2025):

> "Absolutely playable and finishable. I recently finished another run on stream... In its current state, OA is a blast to play and I highly recommend it. Just keep in mind it's still in the Alpha state." — Quickmind, Tester (March 2024)

### What Works

- Full cityscape with building management, vehicle deployment, and aerial combat
- Complete battlescape with real-time and turn-based tactical combat
- All 54+ configurable gameplay options (More Options menu)
- Agent hiring, training, and equipment management
- Research and manufacturing systems
- Organization diplomacy (partially — see known issues)
- Base building and management
- Save/load system (zipped XML format)
- Modding support via XML patches and Lua scripting
- Debug mode and cheat system
- Cross-platform support (Windows, Linux, macOS)

### What Requires Cheats or Workarounds

- **Weekly funding**: The economy system is partially implemented; funding may need manual adjustment
- **Alien dimension access**: Trip to the alien dimension may require debug commands
- **Victory/loss screens**: Not yet implemented

### What's Missing or Incomplete

| Feature | Status | Notes |
|---------|--------|-------|
| **Learning AI** | Not implemented | The OG's neural network AI (BRAIN.DAT/EXPERIEN.DAT/WEAPEXP.DAT) is not replicated. The current tactical AI uses a basic placeholder written by Istrebitel. |
| **Map randomization** | Not implemented | The same map layouts repeat. OG scaled maps by squad size with random variation. |
| **Music engine** | Not implemented | Only a single ambient track plays. OG had dynamic music responding to threat levels. |
| **Victory/loss screens** | Not implemented | Game is winnable but no victory screen appears. |
| **Advanced unit AI** | Partial | Missing: strafing, crouching, prone, false flags, regrouping, reinforcement calls. Beta2 AI was significantly more capable. |
| **Ground vehicle pathfinding** | Barely functional | Can't make corners, drives off roads, all-terrain mode broken. |
| **Agent People Tube usage** | Not implemented | Agents can't use People Tubes for city travel. |
| **Proper jumping** | Incomplete | OG allows jump down + across one tile. OA only goes down a level. |

## The Biggest Technical Challenge: TPS/FPS (Issue #997)

This is the **single most impactful open issue**, extensively discussed from 2019 through 2025.

**The problem**: The original game ran at 36 ticks per second tied to ~18 FPS. OpenApoc runs at 60 FPS, but different parts of the codebase assume different tick rates (36, 60, or 144) depending on which developer wrote them. One developer may have been working on a 144Hz monitor without realizing it was hardware-specific.

**What it affects**: Weapon fire rates, explosion radii, movement speeds, vehicle dynamics, damage calculations, armor calculations, ballistic weight and speed — essentially everything timing-dependent in the game simulation.

**Known consequences**:
- Explosion radius is confirmed "way off" (JonnyH, Feb 2026)
- Autocannon HE/IN/Gas rounds have much larger blast areas than OG
- Smoke persists too long
- Weapon fire rates don't match OG values
- Incendiary and gas dissipation rates differ

**Consensus fix approach**: Incremental — isolate one system at a time, review all timing-dependent calculations, and unify to a consistent TPS value. A monumental task, but no alternative exists.

## Architecture: Strengths and Pain Points

### The StateRef/StateObject System

JonnyH (lead developer) explicitly identified this as the root cause of many bugs:

> "I don't think the StateRef/StateObject system is really that good — it's a mess of pointers and weird shared ownership that relies on things cleaning up all back references 'correctly' every time — the effective source for all 'Missing Object' errors"

A major rework is planned (as of 2025). JonnyH has stated that if starting today, he would use an **Entity Component System (ECS)** instead.

### Serialization

The save/load system is code-generated from `gamestate_serialize.xml`. The generated serialization code is a massive compilation unit requiring 3GB+ RAM to compile. Save games use zipped XML files, which has the benefit of being human-readable and editable.

### State/UI Boundary

A strict separation exists: `game/state/` cannot call into `game/ui/`. This is enforced at the linker level. Events and callbacks are used to communicate between the two layers.

### No Initial Design

The codebase grew organically without a formal design document. Much of it was written concurrently with reverse-engineering efforts, and different developers brought different assumptions about tick rates, ownership patterns, and architectural conventions.

## Reverse Engineering Status

The original X-COM: Apocalypse was compiled with **Watcom C for DOS** using the dos4gw 32-bit extender. It uses two separate executables: `ufop.exe` (cityscape) and `tacp.exe` (battlescape), exchanging data via files.

### What's Been Reversed

| System | Status | Key Contributor |
|--------|--------|-----------------|
| Weapon fire rate formula | Confirmed | skin36 (disassembly) |
| Accuracy RSS model | Confirmed | skin36 (disassembly) |
| AI neural network structure | Confirmed (6-layer MLP) | skin36, Julian Gollop confirmation |
| WEAPEXP.DAT format | Fully documented | skin36 |
| EXPERIEN.DAT structure | Mostly known | skin36, DrNukeLear |
| BRAIN.DAT structure | Partially known | skin36 |
| Transport generation formula | Confirmed | skin36 (disassembly) |
| Organization relation changes | Partially confirmed | skin36 (calc_relation) |
| Explosion mechanics | Active investigation | JonnyH (Feb 2026, Ghidra) |

### Clean Room Policy

The project follows a **clean room reverse-engineering approach**: mechanics are reversed as needed, then new implementations are written from that understanding. No original code is converted verbatim — this is essential for legal protection against Take-Two Interactive.

> "We run clean room, so reversing is done as needed, then new interpretations worked from that. It's the only way to mitigate attentions from Take2." — filmboy84

## The Original Game's Learning AI

One of the most fascinating discoveries from the Discord research:

**Julian Gollop personally confirmed** that X-COM: Apocalypse uses a **neural network** — specifically a 6-layer multilayer perceptron — for its tactical AI. The system evaluates player effectiveness across 25 parameters and adjusts alien behavior accordingly.

Three data files form the AI system:
- **BRAIN.DAT** (555,900 bytes) — Neural network weights
- **EXPERIEN.DAT** (898,776 bytes) — Running statistics, updated every ~12 seconds
- **WEAPEXP.DAT** (34,320 bytes) — Weapon effectiveness tracking

The learning AI was generated through **6,000-8,000 automated battle simulations per map block**. However, it is **broken in most released versions** — save/load resets the decision matrix, and only the original UK/EU CD-ROM release (version 1.03) is confirmed to have it working.

This system has **not been implemented in OpenApoc** and remains one of the most complex outstanding features.

## Known Data Errors in OpenApoc

Our research confirmed several concrete data discrepancies:

| Item | OpenApoc Value | OG Value | Source |
|------|---------------|----------|--------|
| AP Grenade damage | 56 | 48 | skin36 (disassembly) |
| High Explosive damage | 120 | 90 | skin36 (disassembly) |
| Adv. Security Turret beam | Devastator | Disrupter | filmboy84 (testing) |
| Heavy Launcher AG fire delay | 320 | 80 | JonnyH (TICKS_MULTIPLIER bug) |
| AG missile accuracy | 10 | 90 | JonnyH (extractor bug) |

## Modding Ecosystem

OpenApoc supports modding through a layered XML system:
1. **Generated data** (extracted from OG)
2. **Common patch** (`data/common_patch/`)
3. **Difficulty patches** (per-difficulty overrides)
4. **Mod patches** (`data/mods/` with `modinfo.xml`)

The **Extended Weapons Mod (EWM)** by filmboy84 is the primary mod and testing platform, adding UFO/TFTD weapons, new aliens, 2000+ agent names, and balance fixes.

**Limitations**: Damage types are hardcoded (not moddable). Adding a single weapon item takes approximately 12 hours due to the sprite workflow. Difficulty patches load after mods, requiring Lua `onload` scripts for difficulty-dependent mod values.

## Community Health

The project is **alive and active**, though development pace varies:

- **JonnyH** continues core engine work and is actively reverse-engineering the OG in Ghidra (as of Feb 2026)
- **skin36** remains available for reverse-engineering questions
- **filmboy84** continues community management, testing, and mod development
- **Kurtsley** has been actively fixing bugs (relations system, dimension gates, save games) in 2024-2025

The Discord server has **3,352 unique participants** across its history, with active discussions continuing.

### Legal Situation

The project is careful about its legal standing:
> "The problem is the moment any money is made we become a target for Take2. This project is open source and free. Progress is made as and when people work on it for fun and a love of the game." — filmboy84

No Patreon or donations are accepted. The clean room reverse-engineering policy is strictly maintained.

## Roadmap to 1.0

Three GitHub milestones track progress:

| Milestone | Issue | Status |
|-----------|-------|--------|
| **Alpha** | [#263](https://github.com/OpenApoc/OpenApoc/issues/263) | In progress |
| **Beta** | [#264](https://github.com/OpenApoc/OpenApoc/issues/264) | Future |
| **1.0 Release** | [#265](https://github.com/OpenApoc/OpenApoc/issues/265) | Future |

The path to 1.0 requires:
1. Resolving TPS/FPS inconsistency (#997) — affects everything timing-dependent
2. Completing the StateRef/StateObject rework — eliminates "Missing Object" errors
3. Implementing proper tactical AI — the biggest missing feature
4. Map randomization — same maps currently repeat
5. Music engine — only ambient sound exists
6. Economy/funding system completion
7. Victory/loss conditions and screens

New features (beyond OG parity) are deferred until the original game is matched in features and presentation.

## Conclusion

OpenApoc is a remarkable open-source achievement — a playable reimplementation of a complex 1997 strategy game built by a small, dedicated community over nearly a decade. While significant work remains (particularly the TPS fix, AI system, and map generation), the project is in a healthy state with active development and a clear roadmap. The recent discovery that Julian Gollop confirmed the neural network AI adds both historical significance and a fascinating technical challenge for the project's future.

---

*This assessment was compiled in February 2026 from codebase analysis, 50+ GitHub PRs, 77,612 Discord messages spanning 8.3 years, and extensive web research. See [Research Statistics](research-stats.md) for methodology details.*

## See Also

- [Research Statistics](research-stats.md) — How this research was conducted
- [Discord Mining Summary](mining-summary.md) — All 20 critical findings
- [Future Works](future-works.md) — Actionable next steps from this research
- [Roadmap](../openapoc/roadmap.md) — Detailed development roadmap
- [Architecture](../development/architecture.md) — Codebase architecture overview
