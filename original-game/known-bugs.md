# Known Bugs in Original Game (X-COM: Apocalypse)

This document catalogs the significant known bugs in the original X-COM: Apocalypse (1997).
These are important for OpenApoc development because they represent decisions about whether
to faithfully reproduce original behavior or fix long-standing issues.

## Critical Bugs

### Learning AI Broken on Save

**Severity**: Critical
**Area**: Strategic AI

The original game features a "Learning AI" system that is supposed to adapt alien tactics
based on player behavior. However, this system breaks permanently after any save and reload
cycle.

- The Learning AI tracks player patterns (preferred tactics, base locations, response times)
  and adjusts alien behavior accordingly.
- When the game is saved, the Learning AI state is not properly serialized.
- After loading a saved game, the Learning AI resets to its default state and ceases to
  adapt.
- Since virtually all players save their games, the Learning AI effectively never functions
  as intended in normal gameplay.
- This means the AI behavior experienced by most players is the baseline non-adaptive
  behavior.

### Learning AI CD Dependency

**Severity**: Critical
**Area**: Strategic AI / File System

The Learning AI system has a secondary bug related to its data file locations.

- The Learning AI data files are expected to be located on the original CD-ROM at specific
  paths.
- When the game is installed to a hard drive, the AI cannot locate these files on the CD.
- Digital distribution versions (GOG, Steam) do not have a CD-ROM drive, making the files
  entirely inaccessible.
- Even when the CD is present, the file paths may not resolve correctly on modern systems.
- This compounds with the save/load bug to make the Learning AI essentially non-functional
  in all practical scenarios.

### CD-ROM Prompt in Digital Versions

**Severity**: Moderate
**Area**: File System / Compatibility

Digital distribution versions of the game may trigger CD-ROM check prompts.

- The original game was designed to read certain data files from the CD-ROM during gameplay.
- Digital versions bundle these files but may not correctly redirect all file access paths.
- Players may encounter spurious "Insert CD" prompts or file-not-found errors.
- Various community patches and wrapper programs exist to work around this issue.

## Tactical Combat Bugs

### Turn-Based Security Station Turret TU Bug

**Severity**: Moderate
**Area**: Turn-Based Combat / Base Defense

Security Station turrets in base defense missions have a Time Unit (TU) allocation bug in
turn-based mode.

- Security Station and Advanced Security Station turrets are supposed to receive TUs each
  turn to fire at intruding aliens.
- Due to a bug, the TU allocation for turrets is incorrect, often resulting in turrets
  having insufficient TUs to fire.
- This makes Security Station turrets significantly less effective in turn-based base defense
  than they are in real-time mode.
- The bug only affects turn-based mode; in real-time mode, turrets fire continuously and
  normally.

### Brainsuckers Cannot Attack Prone Units

**Severity**: Minor (exploitable)
**Area**: Tactical Combat / Alien AI

Brainsuckers are unable to attach to agents who are in the prone (lying down) position.

- A Brainsucker that reaches a prone agent will fail to attach and may circle uselessly.
- This is not intended behavior; Brainsuckers should be able to attack regardless of the
  target's posture.
- Players can exploit this by ordering agents to go prone when Brainsuckers are nearby,
  rendering the agents immune to Brainsucker attacks.
- This significantly reduces the threat of Brainsuckers for players who know about the bug.

### Overhead View Item Display Corruption

**Severity**: Minor (visual)
**Area**: Tactical Combat / UI

When using the overhead (top-down) tactical view, items on the ground may display incorrectly.

- Items dropped on the battlefield or left by dead units may render with corrupted or
  incorrect sprites in overhead view.
- The items themselves are not actually corrupted; switching to the isometric view shows
  them correctly.
- This is a rendering/display bug only and does not affect gameplay mechanics.
- Items can still be picked up normally regardless of the visual corruption.

### Spitter AI Passive Behavior

**Severity**: Moderate
**Area**: Tactical Combat / Alien AI

Spitter aliens frequently fail to use their ranged acid attack and instead remain passive.

- Spitters are supposed to be ranged attackers that spit acid at X-COM agents from distance.
- Due to an AI pathfinding or targeting bug, Spitters often stand idle or wander without
  attacking, even when valid targets are in range and line of sight.
- This makes Spitters far less dangerous than their stats and intended role would suggest.
- The bug is inconsistent; Spitters sometimes attack normally, but passive behavior is
  common.

### Megaspawn Retreat Behavior

**Severity**: Minor
**Area**: Tactical Combat / Alien AI

Megaspawn units exhibit unintended retreat behavior under certain conditions.

- Megaspawn are the heaviest alien combat units and are designed to be aggressive
  front-line fighters.
- Under certain damage thresholds or tactical conditions, Megaspawn will retreat from combat
  instead of pressing their attack.
- This is inconsistent with their intended role as relentless heavy assault units.
- The retreat behavior can make Megaspawn encounters easier than intended, as they
  disengage rather than using their superior HP and firepower.

## Inventory and Equipment Bugs

### Employee Sacking Bug

**Severity**: Moderate
**Area**: Personnel Management

Firing (sacking) employees can incorrectly dismiss additional personnel beyond the intended
target.

- When the player fires an agent or staff member from the personnel screen, the game may
  also fire one or more additional employees.
- The extra dismissals appear to be related to list indexing errors in the personnel
  management code.
- This can result in the unintentional loss of valuable experienced agents or scientists.
- Players who are aware of this bug often save before any personnel management actions.

### Brainsucker Pod Zero Ammo Save Corruption

**Severity**: High
**Area**: Save System / Equipment

Brainsucker Pods with zero remaining ammunition can cause save file corruption.

- When a Brainsucker Pod (the alien weapon that launches Brainsuckers) has expended all
  its ammunition (zero Brainsuckers remaining), the item enters an invalid state.
- If the game is saved while a zero-ammo Brainsucker Pod exists in any inventory (agent,
  ground, storage), the save file may become corrupted.
- Corrupted save files may crash on load or exhibit unpredictable behavior.
- The workaround is to dispose of empty Brainsucker Pods before saving (drop and leave them
  on the battlefield).

### Inventory Screen Lock

**Severity**: Minor
**Area**: Tactical Combat / UI

The agent inventory screen can become locked or unresponsive under certain conditions.

- During tactical combat, accessing an agent's inventory screen may occasionally result in
  the screen becoming unresponsive to input.
- The exact trigger is unclear but may be related to attempting to manipulate items while
  the agent is performing another action.
- The lock can sometimes be resolved by pressing Escape or clicking outside the inventory
  window; in severe cases, the game may need to be reloaded from a save.

## Community-Discovered Bugs

The following bugs were identified through OpenApoc Discord community research, reverse
engineering, and extensive playtesting.

### GOG Mismatched Executables

**Severity**: Critical
**Area**: Distribution / Compatibility

The GOG distribution of X-COM: Apocalypse ships with mismatched executables:

- **UFOEXE** (cityscape executable) is actually the renamed **486 version**.
- **TACEXE** (tactical executable) is the **Pentium 1 version**.

This mismatch leads to crashes to desktop (CTDs) during gameplay, particularly when
transitioning between the cityscape and tactical layers. Community report:
https://www.gog.com/forum/xcom_series/xcom_apocalypse_serious_distribution_bug_please_fix_gog

### Learning AI Save/Load Bug (Extended Details)

**Severity**: Critical
**Area**: Strategic AI

In addition to the previously documented save/load behavior, community research has confirmed
that this bug is **not present in beta/debug versions** of the original executable. This
suggests the bug was introduced during final release preparation, possibly as an unintended
side effect of removing debug instrumentation.

### Midnight / City Repair Freeze

**Severity**: High
**Area**: Strategic Layer / City Simulation

The game can **freeze after midnight** during the city repair/update cycle. According to
community testing, the workaround is to **damage a building** before midnight passes, which
forces the repair logic into a code path that avoids the freeze condition.

### Agent Firing Bug (Over 20 Agents)

**Severity**: Moderate
**Area**: Personnel Management

When X-COM employs **more than 20 agents**, firing (sacking) one agent can cause a
**different agent to be fired instead**, potentially from a completely different role
(e.g., firing a soldier removes a scientist). This is related to but distinct from the
previously documented Employee Sacking Bug, and specifically triggers with large rosters.

### Building Replacement Bug

**Severity**: Moderate
**Area**: Base Management

**Transferring engineers** between bases can trigger a bug where a base **facility is
incorrectly replaced** by a different facility type. The exact trigger conditions involve
the engineer transfer coinciding with facility construction or demolition operations.

### Mind Shield Permanent Stat Boost Exploit

**Severity**: Minor (exploitable)
**Area**: Equipment / Stats

Holding a **Mind Shield through mission end** grants a **permanent psi-defense boost** to the
agent's base stats. This is cumulative across multiple missions. See
[psionics.md](psionics.md) for details.

### 1-Turn Final Mission Exploit (TB Mode)

**Severity**: Minor (exploitable)
**Area**: Turn-Based Combat / Campaign

In turn-based mode, the **final mission can be completed in a single turn** by exploiting
specific movement and action sequences. This bypasses most of the intended challenge of the
final alien dimension assault.

### Workshop Infinite Money Exploit

**Severity**: Minor (exploitable)
**Area**: Manufacturing / Economy

According to community testing, certain manufacturing workflows can be manipulated to
generate **unlimited money** through workshop production. The exact mechanism involves
exploiting price calculations or production queue manipulation.

### Stun Raid Economy Exploit

**Severity**: Minor (exploitable)
**Area**: Tactical Combat / Diplomacy

In the original game, conducting **stun raids** (raiding buildings using only stun weapons
to incapacitate rather than kill) incurs **no relationship penalty** with the targeted
organization. This allows the player to repeatedly raid organizations for equipment and
funds without diplomatic consequences, which is clearly unintended behavior.

### Scientists/Engineers in Base Defense

**Severity**: Moderate
**Area**: Base Defense / Personnel

When a base has **too many scientists or engineers present**, they may **appear in base
defense missions instead of combat agents**. Scientists and engineers have no combat training
and minimal equipment, making them ineffective defenders and easy casualties.

## OpenApoc Relevance

These bugs are documented for OpenApoc developers to make informed decisions about:

1. **Bug-for-bug compatibility**: Some players expect original behavior, even if bugged.
2. **Intentional fixes**: Most of these bugs should be fixed in OpenApoc, as they detract
   from the intended gameplay experience.
3. **Configurable behavior**: For controversial cases, a configuration option could allow
   players to choose between original and fixed behavior.

## Sources

- [Bugs (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Bugs_(Apocalypse))
- [Known Bugs (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Known_Bugs_(Apocalypse))
- [Learning AI (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Learning_AI_(Apocalypse))
- [Brainsucker (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Brainsucker_(Apocalypse))
