# Base Building (X-COM: Apocalypse)

This document covers the base building system in the original X-COM: Apocalypse (1997).
Unlike previous X-COM games where bases are built underground in remote locations, Apocalypse
bases are constructed inside purchased buildings within the Mega-Primus cityscape.

## Base Acquisition

X-COM bases are established by purchasing existing buildings in Mega-Primus from their
owning organizations. Once purchased, the building's interior is converted into a modular
base layout where facilities can be constructed.

- **Starting Base**: X-COM begins with one pre-built base containing basic facilities.
- **Additional Bases**: New bases can be established by purchasing buildings from willing
  organizations. The building's size determines the available construction footprint.
- **Location Matters**: Base location within the city affects response times to alien
  incursions and proximity to organizational assets.
- **Cost**: Building purchase prices vary based on size, location, and the owning
  organization's relationship with X-COM.

## Facilities

Facilities are constructed within the base grid. Each facility occupies one or more grid
squares and provides specific functions. Construction takes time and money.

### Personnel Facilities

| Facility          | Size  | Function                                                          |
|-------------------|-------|-------------------------------------------------------------------|
| Living Quarters   | Small | Houses agents and staff. Required to employ personnel at the base. Each module provides a fixed number of living spaces. |
| Medical Bay       | Small | Treats injured agents, accelerating recovery time. Agents assigned here heal faster than those without medical care. |
| Training Area     | Small | Trains agents' physical stats: Strength, Reactions, Stamina, and Health. Agents must be assigned to train. |
| Psi-Gym           | Small | Trains agents' psionic stats: Psi-Attack, Psi-Defence, and Psi-Energy. Only effective for agents with existing psionic ability. |

### Research Facilities

| Facility                   | Size  | Function                                                     |
|----------------------------|-------|--------------------------------------------------------------|
| Biochemistry Lab           | Small | Workspace for Biochemist scientists. Required for all Biochemistry research projects. |
| Advanced Biochemistry Lab  | Large | Upgraded Biochemistry workspace. Holds more scientists per facility than the standard lab. |
| Quantum Physics Lab        | Small | Workspace for Quantum Physicist scientists. Required for all Quantum Physics research. |
| Advanced Quantum Physics Lab | Large | Upgraded Quantum Physics workspace. Holds more scientists per facility. |

### Manufacturing Facilities

| Facility            | Size  | Function                                                        |
|---------------------|-------|-----------------------------------------------------------------|
| Workshop            | Small | Workspace for Engineers. Required for all manufacturing projects. |
| Advanced Workshop   | Large | Upgraded manufacturing workspace. Holds more engineers per facility. Enables production of some advanced items. |

### Storage and Vehicle Facilities

| Facility          | Size  | Function                                                          |
|-------------------|-------|-------------------------------------------------------------------|
| Storage           | Small | Stores equipment, weapons, ammunition, alien artifacts, and materials. Each module provides a fixed storage capacity. |
| Vehicle Hangar    | Large | Houses and launches X-COM vehicles. Each hangar accommodates a limited number of vehicles depending on their size. |
| Repair Bay        | Large | Repairs damaged vehicles. Vehicles assigned to a Repair Bay recover HP over time. |

### Alien Containment

| Facility              | Size  | Function                                                      |
|-----------------------|-------|---------------------------------------------------------------|
| Alien Containment     | Small | Holds live captured aliens for research. Required to perform autopsies and maintain live specimens. Aliens die if containment is lost. |

### Security Facilities

| Facility                    | Size  | Function                                                  |
|-----------------------------|-------|-----------------------------------------------------------|
| Security Station            | Small | Provides automated turret defense during base defense missions. Turrets engage hostile units within the base. |
| Advanced Security Station   | Small | Upgraded security turrets with improved damage and durability. |

**Note**: In turn-based mode, Security Station turrets have a known TU bug that can impair
their effectiveness. See [known-bugs.md](known-bugs.md) for details.

## Facility Limits

The game imposes limits on certain facility types to prevent excessive stacking:

- **Maximum 6 small labs/workshops** per base (Biochemistry Lab, Quantum Physics Lab,
  Workshop).
- **Maximum 4 large labs/workshops** per base (Advanced Biochemistry Lab, Advanced Quantum
  Physics Lab, Advanced Workshop).
- These limits mean a single base cannot house an unlimited number of scientists or
  engineers. Multiple bases are needed for large-scale research and manufacturing operations.

## Base Layout and Construction

### Construction Grid

Each base has a fixed grid layout determined by the purchased building's size. Facilities
are placed on this grid:

- Small facilities occupy a single grid square.
- Large facilities occupy multiple grid squares (typically 2x2).
- Facilities cannot overlap.
- The grid must have connected access paths; isolated facilities may not function properly.

### Construction Time

- Each facility has a construction time measured in days.
- Construction requires a monetary cost paid upfront.
- Only one facility can be under construction at a time per base (in most cases).
- Demolishing facilities also takes time but refunds a portion of the cost.

## Base Defense

When aliens attack an X-COM base, a tactical base defense mission is triggered. The base
layout directly affects the defensive battle:

- **Facility placement** determines the tactical map. The physical layout of your facilities
  becomes the battlefield.
- **Security Stations** provide automated turret support during defense missions.
- **Chokepoints**: Careful facility placement can create defensive chokepoints that funnel
  attackers into kill zones.
- **Access lifts**: Connections between base sections determine how both defenders and
  attackers can move through the base.

## Multi-Base Strategy

Experienced players typically operate multiple bases for different purposes:

- **Primary Base**: Research-heavy with maximum lab facilities, Alien Containment, and
  Living Quarters for scientists.
- **Manufacturing Base**: Workshop-heavy for producing equipment and generating profit.
- **Forward Operating Bases**: Smaller bases with hangars and living quarters positioned
  for rapid response to alien activity in distant parts of the city.
- **Training Base**: Equipped with Training Areas and Psi-Gyms for developing new recruits.

## Sources

- [Base Facilities (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Base_Facilities_(Apocalypse))
- [Base Defense (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Base_Defense_(Apocalypse))
- [Bases (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Bases_(Apocalypse))
