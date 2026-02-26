# Shared Mechanics Between OpenApoc and X-COM: Apocalypse

OpenApoc aims to be a faithful reimplementation of X-COM: Apocalypse. The vast majority of core game mechanics are intentionally preserved to match the original game's behavior as closely as possible. This page documents the fundamental systems that work the same (or very nearly the same) in both games.

## Core Combat Mechanics

### Damage Calculation

The base damage calculation system is preserved from the original game. When a projectile hits a target:

- Base damage is determined by the weapon's power rating.
- Damage is randomized within the Apocalypse damage model range (by default; an optional X-COM 1 style 0-200% model is also available as a toggle).
- Armor reduces incoming damage based on the armor value of the hit location.
- Damage types (kinetic, incendiary, explosive, etc.) interact with armor types through the same damage modifier table used in the original.

### Unit Actions

The fundamental unit action system is the same:

- **Movement**: Units move on a tile-based grid with the same movement costs for different terrain types and stances (standing, kneeling, prone).
- **Firing**: Aimed, snap, and auto fire modes function as in the original, with accuracy modified by the same factors (agent stats, weapon accuracy, range, stance).
- **Throwing**: Grenade and item throwing uses the same arc calculation and range limitations.
- **Psionic combat**: Psi attacks use the same stat-based success formula comparing attacker psi-energy/attack against defender psi-energy/defense.
- **Time Units**: In turn-based mode, actions consume TUs using the same cost formulas as the original game.

### Health and Wounds

- Hit points, fatal wounds, stun damage, and morale all use the same underlying mechanics.
- Fatal wounds drain health at the same rate per turn.
- Stun damage accumulation and recovery follow the original formulas.
- Morale checks and panic/berserk thresholds match the original behavior.

## Organization System

### Relationships

The inter-organization relationship system functions as in the original:

- Organizations have relationships with each other and with X-COM, ranging from Allied to Hostile.
- Actions taken by X-COM (attacking vehicles, raiding buildings, collateral damage) affect relationships using the same reputation change values.
- Organizations can become hostile to X-COM or to each other based on accumulated relationship changes.
- Alien infiltration degrades organization loyalty over time following the same progression curve.

### Organization Activities

- Organizations buy and sell goods on the open market.
- Organizations own buildings, vehicles, and agents.
- Inter-organization conflicts (raids, vehicle combat) occur based on the same relationship triggers.
- Organizations provide funding to X-COM based on their relationship level.

## Base Building

### Facility Construction

- The base layout grid, facility sizes, and placement rules are the same.
- Construction times for each facility type match the original.
- Facility functions (living quarters capacity, lab space, workshop space, storage, containment) use the same values.
- Base defense mechanics in tactical combat use the same map generation approach (base layout maps to tactical tileset).

### Base Management

- Agent hiring, vehicle purchasing, and equipment procurement use the same market system.
- Transfer times between bases follow the same calculation.
- Base upkeep costs match the original values.

## Research and Manufacturing

### Research

- Research topics, prerequisites, and dependency chains are preserved from the original data.
- Research progress is calculated using the same formula: number of assigned scientists multiplied by their skill, accumulated over time.
- Lab size requirements (quantum physics vs. biochemistry) match the original.
- UFOpaedia entries unlock upon research completion following the same triggers.

### Manufacturing

- Manufacturing topics, costs, and time requirements match the original data.
- Workshop space and engineer assignment mechanics are the same.
- Manufacturing prerequisites (required research) follow the original dependency tree.
- Produced items are added to base stores using the same logic.

## Alien Invasion Progression

### Weekly Escalation

- The alien invasion escalates over time following the same weekly progression schedule.
- UFO types and mission patterns advance according to the same timeline.
- Alien infiltration of organizations follows the same mechanics -- aliens send infiltration missions, and organizations gradually become compromised.

### Alien Species

- All original alien species are present: Brainsuckers, Multiworms (and their lifecycle stages), Anthropods, Skeletoids, Spitters, Poppers, Psimorphs, Megaspawn, Micronoids, and Queenspawn.
- Alien stats, equipment, and behavioral characteristics match the original game data.
- The alien lifecycle (eggs to multiworms to hyperworms/chrysalis) follows the same progression.

### Alien Dimension

- The Alien Dimension is accessible through dimension gates as in the original.
- Alien building types and their functions match the original.
- The overall mission structure for attacking the alien dimension is preserved.

## Map Structure and Tactical Combat

### Map Generation

- Tactical maps are generated from the same tileset system as the original game.
- Building interiors use the same sectored map assembly approach: buildings are composed of map sections (SECs) assembled according to the building type's rules.
- Terrain destruction follows the same support-based collapse mechanics -- destroying load-bearing elements causes sections above to fall.

### Line of Sight

- Line-of-sight calculations use tile-based visibility checks consistent with the original game's approach.
- Vision range and the 90-degree field of view cone are preserved.
- Smoke and fire provide vision obstruction using the same blocking values.

### Pathfinding

- Units pathfind through the 3D tile grid using similar algorithms.
- Movement costs for different terrain types, elevation changes, and obstacles match the original.
- Flying units, ground units, and different movement modes (walk, run, prone) use the same movement cost multipliers.

## Agent System

### Recruitment

- Agents are recruited from the same pool of types: human soldiers, androids, and hybrids.
- Each agent type has the same base stat ranges and growth potential as in the original.
- Agent stats (strength, accuracy, reactions, bravery, psi-energy, psi-attack, psi-defense, health, TUs, stamina, speed) use the same value ranges.

### Stat Growth

- Agent stats improve through combat experience using the same growth mechanics.
- The stat that improves depends on the action performed (firing improves accuracy, taking damage can improve bravery, etc.).
- Maximum stat caps match the original values.

### Equipment

- All original weapons, armor, and equipment items are present with their original stats.
- Inventory slot system (right hand, left hand, body slots, belt slots) matches the original.
- Equipment weight affects TU costs using the same formula.

## Vehicle System

### Vehicle Types

- All original vehicle types are available: hovercars, hoverbikes, interceptors, transports, and ground vehicles.
- Vehicle stats (speed, acceleration, armor, cargo capacity, passenger capacity) match the original data.
- Vehicle equipment slots and compatible equipment types follow the original configurations.

### Aerial Combat

- Vehicle-to-vehicle combat uses the same engagement mechanics.
- Weapon ranges, damage values, and accuracy follow the original data.
- Shield and armor mechanics for vehicles match the original.
- UFO interception and crash/landing site generation follow the same rules.

## Economy

### Funding

- Weekly government funding follows the same base amount and relationship-based modifiers.
- Score calculations that affect funding use the same point values for kills, recoveries, and mission success/failure.

### Market

- Equipment prices and availability follow the original market data.
- Market stock replenishment rates match the original values.
- Organization-specific purchasing restrictions are preserved.

## Note on Fidelity

OpenApoc's primary goal is faithful recreation of the original game experience. Where the original game's behavior has been clearly documented (through reverse engineering, community research, or observable gameplay), OpenApoc strives to match it exactly. Deviations from the original are typically:

1. **Bug fixes** -- correcting clearly broken behavior (see [Bug Fixes](bug-fixes.md)).
2. **Optional enhancements** -- new features that can be toggled off (see [Differences](differences.md)).
3. **Unfinished features** -- mechanics not yet implemented in the current alpha state.

When in doubt about whether a specific mechanic matches the original, check the [Differences to X-COM](differences.md) page or ask on the [OpenApoc Discord](https://discord.gg/f8Rayre).

## See Also

- [Differences to X-COM](differences.md) -- what OpenApoc changes or adds
- [Bug Fixes](bug-fixes.md) -- original game bugs that OpenApoc corrects
- [X-COM: Apocalypse on UFOpaedia](https://www.ufopaedia.org/index.php?title=Apocalypse) -- comprehensive original game reference
