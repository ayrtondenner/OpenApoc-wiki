# Original Game Bugs Fixed by OpenApoc

OpenApoc fixes or works around several [known bugs](https://www.ufopaedia.org/index.php?title=Known_Bugs_(Apocalypse)) present in the original X-COM: Apocalypse (1997). This page documents each bug, its impact in the original game, and how OpenApoc addresses it.

## UFO Speed Bug

**Original bug**: Under certain conditions, alien craft would be assigned a speed value of 0 after being generated or loaded from a save game. This made them stationary and trivially easy to intercept, eliminating any challenge from aerial combat encounters with affected craft.

**OpenApoc fix**: Vehicle speed values are correctly initialized and maintained across save/load cycles. Alien craft always move at their intended speeds as defined in the game data.

## Infiltration Screen Overflow

**Original bug**: The infiltration progress screen would go completely blank after approximately 42 days of in-game time. This was caused by an integer overflow in the display logic -- the infiltration percentage value exceeded the range that the rendering code could handle, resulting in nothing being drawn.

**OpenApoc fix**: The infiltration screen uses proper data types and rendering logic that can handle arbitrarily long game durations without display corruption.

## Security Station Turret TU Bug

**Original bug**: In turn-based combat mode, Security Station turrets (automated base defense weapons) did not have their Time Units refreshed at the start of each turn. After firing once (consuming their initial TUs), they would be unable to act for the remainder of the battle, making them nearly useless as a defensive measure.

**OpenApoc status**: Partially fixed. Turret TU refresh logic has been improved, but the fix may not cover all edge cases in the original turret behavior. Further work is tracked in the project's issue tracker.

## OGG Vorbis Music Playback Issues

**Original bug**: The original game's audio system could produce clicks, pops, stuttering, and other playback artifacts, particularly with music tracks. This was a consequence of the DOS-era audio engine and its limited buffering capabilities.

**OpenApoc fix**: OpenApoc uses SDL2 for audio playback with modern buffering and mixing. Music is decoded via libvorbis, and separate volume controls for music and sound effects are provided. Playback is smooth and free of the artifacts that plagued the original.

## Learning AI Non-Functional

**Original bug**: X-COM: Apocalypse was advertised as featuring a "learning AI" that would adapt alien tactics based on player behavior. In practice, this feature was effectively non-functional:

- The AI learning state was not preserved when saving and loading the game, resetting any accumulated data.
- The system depended on specific CD-ROM file locations that were not reliably accessible.
- Even when technically operational, the behavioral changes were minimal and difficult to observe.

**OpenApoc status**: OpenApoc does not attempt to replicate this broken feature. The alien AI uses consistent, well-defined behavior patterns instead. Implementing a functional learning AI system remains a potential future enhancement but is not a priority for the current alpha milestone.

## Brainsucker Pod Issues

**Original bug**: Brainsucker Pods had multiple inventory and storage-related bugs in the original game:

- Pods could sometimes become stuck in agent inventory slots, unable to be removed or used.
- Storage space calculations for Brainsucker Pods were incorrect, leading to discrepancies between reported and actual storage usage.
- The alien containment display could show incorrect counts when Brainsuckers were involved.
- Transferring Brainsucker Pods between bases could trigger inconsistencies.

**OpenApoc fix**: Inventory handling for Brainsucker Pods uses the same standardized item management system as all other equipment, eliminating the special-case bugs present in the original. Storage calculations and containment displays correctly account for all item types.

## Crash Fixes and Stability Improvements

OpenApoc addresses numerous crash conditions that existed in the original game or that emerged during reimplementation. Notable categories include:

### Save/Load Stability

- Eliminated crashes when loading save games with corrupted or missing vehicle references.
- Fixed crashes related to organization state inconsistencies after loading.
- Save games use a human-readable XML format in ZIP archives, making them inspectable and recoverable if issues occur.

### Combat Stability

- Fixed crashes when units attempt to pathfind to unreachable locations.
- Resolved null pointer issues when units interact with destroyed map objects.
- Fixed crashes related to projectile collision detection at map boundaries.
- Addressed memory issues with large tactical maps and many active units.

### City Management Stability

- Fixed crashes when buildings are destroyed while vehicles are en route.
- Resolved issues with vehicle management when organizations are eliminated.
- Fixed crashes related to market transactions with unavailable items.

## Additional Minor Fixes

- **Dimension gate visuals**: Fixed rendering issues with dimension gate effects that could cause visual artifacts.
- **Scroll bar behavior**: Fixed UI scroll bars that could become unresponsive or jump to incorrect positions in long lists.
- **Unit facing**: Corrected cases where units would face incorrect directions after completing certain actions.
- **Equipment screen**: Fixed display issues when agents carried items of unusual sizes.

## Discord-Mined Bug Fixes

The following additional bug fixes have been identified through OpenApoc Discord community discussion. These address either OG bugs that OpenApoc has corrected or OpenApoc-specific issues that have been resolved.

### Prone Brainsucker Immunity (OG Bug Fixed)

In the original game, agents lying in the **prone position** were completely immune to brainsucker attacks. This was an unintended exploit -- players could order all agents to go prone to trivialise any encounter involving brainsuckers. OpenApoc has fixed this bug: brainsuckers can now successfully attack prone agents, making brainsucker encounters a genuine tactical threat regardless of agent stance.

### Stun Raiding Economy Exploit

The OG allowed players to exploit the stun mechanic for economic gain by repeatedly stunning and raiding organisation personnel without meaningful diplomatic consequences. OpenApoc addresses this via the **"Stunning hurts relationships"** mod option (`OpenApoc.Mod.StunHostileAction`). When enabled, stunning units belonging to an organisation damages X-COM's relationship with that organisation, closing the exploit loop.

### Weekly Loop Timing Fix

The weekly game loop (which triggers funding assessments, economy updates, and UFO growth) was running on **Tuesday** instead of **Monday** as in the OG. This was identified and fixed by contributor Ankor, aligning the weekly cycle with the original game's timing.

### Turn-Based Turret Awareness (Known OG Bug)

In the OG's turn-based mode, Security Station turrets only functioned for the **first 25 TU** of the end-turn phase. After expending those initial Time Units, turrets would become inert for the remainder of the battle. This is a known OG bug that is partially addressed in OpenApoc (see also the [Security Station Turret TU Bug](#security-station-turret-tu-bug) section above).

---

## Reporting New Bugs

If you encounter a bug in OpenApoc, please report it on the [GitHub issue tracker](https://github.com/OpenApoc/OpenApoc/issues). Include:

1. A description of what happened and what you expected to happen.
2. Steps to reproduce the issue.
3. Your save game file (the `.zip` file from your saves directory) if applicable.
4. Your OpenApoc version or build number.

## See Also

- [Differences to X-COM](differences.md) -- full list of differences between OpenApoc and the original
- [Known Bugs (Apocalypse)](https://www.ufopaedia.org/index.php?title=Known_Bugs_(Apocalypse)) -- UFOpaedia page documenting original game bugs
- [OpenApoc Issues](https://github.com/OpenApoc/OpenApoc/issues) -- current bug tracker
