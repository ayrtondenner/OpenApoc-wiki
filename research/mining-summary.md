# Discord Knowledge Mining Summary

## Overview
- Date mined: February 2026
- Source: OpenApoc Discord server (142798944970211328)
- Channels mined: 25 exported (10 failed — archived/restricted)
- Total data: 121 MB of JSON
- Date range of messages: January 2016 through February 2026

## Key Contributors
| Name | Discord Handle | Role | Expertise |
|------|---------------|------|-----------|
| JonnyH | jonnyh | Lead Developer | Engine architecture, rendering, backend |
| filmboy84 | [OpenApoc] Warp Turtle Of Malal | Administrator/Mod Developer | OG game historian, EWM mod, beta versions |
| skin36 | evil wizard | Developer/Reverse Engineer | Disassembled OG executables, formulas, AI files |
| SupSuper | SupSuper | Developer | OpenXCOM lead, data formats |
| Bluddy | Bluddy | Programmer | Got Julian Gollop's neural network confirmation |
| Kurtsley | Kurtsley | Programmer | Dimension gates, tick rate fixes, relations |
| Istrebitel | Istrebitel | Developer | Wrote placeholder tactical AI |
| Zigmar | Zigmar | Programmer | Save game debugging, container safety |
| Flacko | Flacko | Programmer | Cheat menu, AppVeyor, vehicle fixes |
| Thaddaeus Frogley | (external) | Original Apocalypse Developer | Collapsing terrain, procedural dimensions, org allegiance |
| Ayrton Denner | ayrtondenner | Programmer/Documentation/QA | Bug fixes, new features, wiki creation, Discord mining, QA testing, documentation overhaul |

## Critical Findings

### 1. Neural Network AI (HIGH confidence — confirmed by Julian Gollop)
- OG uses 6-layer multilayer perceptron for tactical AI
- Three data files: BRAIN.DAT (555,900 bytes), EXPERIEN.DAT (898,776 bytes), WEAPEXP.DAT (34,320 bytes)
- SAVEGAME.00 = save data (448,300) + all three AI files concatenated
- AI evaluates player on 25 parameters
- Activation function uses erf() (error function), not standard sigmoid
- Generated through 6,000-8,000 automated battle simulations per map block
- Largely broken in released versions — breaks on save/load, new game start, ISO mounting

### 2. TPS/FPS Inconsistency (Issue #997) — THE biggest open issue
- OG: 36 ticks/sec (some calcs use 18)
- OpenApoc: 60 FPS but code assumes 36/60/144 depending on developer
- Affects: weapon fire rates, explosion radii, movement, damage, armor, ballistics
- Root cause: a developer may have been working on 144hz monitor
- Consensus fix: incremental, one system at a time

### 3. Fire Rate Formula (HIGH confidence — from disassembly)
`fire_rate = random(fire_delay) + fire_delay/2`
Recalculated before each shot. Fire delay is constant per weapon.

### 4. Accuracy Formula (HIGH confidence — confirmed by skin36)
RSS of inaccuracy terms: sqrt(agent^2 + weapon^2 + health^2 + wound^2 + berserk^2 + cloak^2)
- Dual-wield penalty: 1.4x if either item > 2x2
- Target size bonus: 1.4x for targets > size 4
- Uses logarithms for deviation angle computation

### 5. TICKS_MULTIPLIER Double-Conversion Bug
Data extractor multiplies fire_delay by TICKS_MULTIPLIER but game update() already does this. Causes double conversion — e.g., Heavy Launcher AG: OG=80, OA=320.

### 6. Explosion Radius "Way Off" (confirmed Feb 2026)
Autocannon HE/IN/Gas much larger in OA. Smoke persists too long. Tied to tick rate issue.

### 7. Grenade Damage Values Wrong
- AP Grenade: OA=56, OG=48
- High Explosive: OA=120, OG=90

### 8. Organization Relations System
- 4 values per pair: short-term + long-term, bidirectional
- Changes via calc_relation(time, org, -5 or -15)
- Short-term updated at midnight
- Three copies in save games
- Alliance system cut: required >25 friendship + 2+ common enemies

### 9. Transport Generation Hourly Distribution
`4,2,2,2,2,2,4,8,12,8,6,4,10,8,6,4,4,12,12,8,4,4,4,4`
Lower at night, peaks in morning/evening rush.

### 10. Shield Mechanics
- Projectiles bypass shields; energy weapons don't
- Shields protect against explosions but not environmental fire
- No protection against toxins or swords

### 11. Agent Recruitment Rates
Daily max hires: Human=3, Android=1, Hybrid=1
- Requires good relations with S.E.L.F. (androids) and Mutant Alliance (hybrids)
- 50 engineer hard cap per category

### 12. Training/Healing Facility Efficiency
80% utilization > 100% full > 120% overworked
Rate tied to TPS value with modifiers.

### 13. Real-Time vs Turn-Based
- Game designed for RT; TB added late
- Turrets only work in RT
- Brainsuckers don't instantly hatch in TB
- 25% TU cap on reaction fire in TB
- Entropy launcher useless in TB but devastating in RT

### 14. Cut Features (from original developer Thaddaeus Frogley)
- Procedural alien dimension with multiple dimensions connected by portals (killed by Microprose QA costs)
- Collapsing terrain (his idea — Gollop brothers doubted it was possible)
- Transport tube network / population movement
- Organization allegiance system
- ~30 alien types proposed, only 14 shipped
- Game started as Judge Dredd game

### 15. StateRef/StateObject Architecture Problem
- Root cause of all "Missing Object" errors
- JonnyH: "if starting today, would use ECS"
- Big rework planned (2025)
- game/state cannot call game/ui directly

### 16. Modding System Architecture
- Layered XML: generated → common_patch → difficulty patch → mods
- gamestate_common is extensionless ZIP
- Mods only need changed values (additive patching)
- Difficulty patches load AFTER mods — use Lua onload scripts for difficulty-dependent mod values
- Damage types are hardcoded, not moddable
- Sprite workflow: ~12 hours per weapon item

### 17. Original Game Versions
- Debug: late 1996/early 1997
- Beta 1: ~April 1997
- Beta 2: 12 June 1997
- Version 1.03: only version with confirmed working learning AI
- GOG has mismatched executables (486 vs Pentium 1) causing mid-game CTDs
- Two executables: ufop.exe (city) + tacp.exe (tactical)
- Compiled with Watcom C for DOS, uses dos4gw extender

### 18. Known Bugs and Exploits (OG)
- Learning AI save/load reset bug
- Midnight/city repair freeze
- Prone brainsucker immunity (fixed in OpenApoc)
- Mind Shield permanent psi stat boost
- 1-turn final mission exploit (TB)
- Workshop infinite money
- Stun raid economy exploit
- Agent firing bug (>20 agents)
- Scientists/engineers appear in base defense

### 19. Voxel/LOFTemps System
- UFO/TFTD: 16x16x24 per tile
- Apocalypse: 32x32x32, 64x64x64, or 32x32x64 depending on tile type
- Single ray to target voxel (degenerate cases possible)
- GCC PGO gives ~5x speedup on raycasting

### 20. Key Reference Links
- Wong's Guide: https://gamefaqs.gamespot.com/pc/36014-x-com-apocalypse/faqs/1731
- WEAPEXP.DAT: https://www.ufopaedia.org/index.php/WEAPEXP.DAT_(Apocalypse)
- EXPERIEN.DAT: https://www.ufopaedia.org/index.php/EXPERIEN.DAT_(Apocalypse)
- BRAIN.DAT: https://www.ufopaedia.org/index.php/BRAIN.DAT_(Apocalypse)
- Cut mechanics: https://www.ufopaedia.org/index.php/Cut_mechanics_and_behavior_(Apocalypse)
- Image formats: https://www.ufopaedia.org/index.php/Image_Formats_(Apocalypse)
- Terry Greer's page: http://www.terrygreer.com/xcomapocalyse.html
- Thaddaeus Frogley's portfolio: http://thad.frogley.info/portfolio/apocalypse.html
- Ghidra LX loader: https://github.com/yetmorecode/ghidra-lx-loader
- Unit AI behaviors: https://openapoc.org/forum/threads/unitai-unit-and-organisation-behaviours.185/
- Learning AI thread: https://openapoc.org/forum/threads/apocalypses-learning-ai.257/
- GOG bug report: https://www.gog.com/forum/xcom_series/xcom_apocalypse_serious_distribution_bug_please_fix_gog

## Channels by Value

| Channel | Size | Value | Key Content |
|---------|------|-------|-------------|
| reversing | 1.8 MB | HIGHEST | Formulas, disassembly, AI files, tick rates |
| alien-infiltration-and-ufo-mechanics | 168 KB | HIGHEST | Focused infiltration/UFO mechanics |
| coding | 9.9 MB | HIGH | Architecture, TPS issue, StateRef, relations |
| general_original_game | 16 MB | HIGH | Game mechanics, strategies, bugs, cut features |
| data | 713 KB | HIGH | Data formats, AI file structures |
| mod_development | 10.7 MB | MEDIUM | Modding techniques, EWM, XML structure |
| testing_bugtracking | 4.8 MB | MEDIUM | Bug patterns, OG vs OA differences |
| general_openapoc | 45 MB | MEDIUM | Installation, status, FAQ, pinned references |
| tools | 323 KB | LOW | Tool-related |
| translations | 1.9 MB | LOW | Translation work |
