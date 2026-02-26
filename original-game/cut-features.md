# Cut Features (X-COM: Apocalypse)

This document catalogs features that were planned for the original X-COM: Apocalypse (1997)
but were cut before release due to time constraints, technical limitations, or design
changes. These cut features are relevant to OpenApoc development because some may be
candidates for future implementation.

## Espionage System

The most significant cut feature was a fully designed espionage system that would have
allowed X-COM to conduct covert operations against Mega-Primus organizations.

### Planned Spy Skills

Agents assigned to espionage roles were intended to have a separate skill set:

| Skill          | Planned Function                                                           |
|----------------|---------------------------------------------------------------------------|
| Identity       | Ability to assume false identities and blend into target organizations. Higher skill meant longer before discovery. |
| Stealth        | Ability to move undetected within hostile buildings. Determined success of covert infiltration and exfiltration. |
| Information     | Ability to gather intelligence about an organization's activities, inventory, finances, alien infiltration level, and planned actions. |
| Theft          | Ability to steal equipment, funds, or technology from target organizations without detection. |
| Assassination  | Ability to eliminate specific individuals within target organizations, including leaders and key personnel. |

### How It Would Have Worked

- Agents would be assigned to "spy missions" at specific organizations, similar to how
  agents are assigned to tactical missions.
- Spy missions would have run in the background during the strategic layer, with outcomes
  determined by skill checks.
- Discovery during a spy mission would damage relations with the target organization and
  potentially result in the agent's capture or death.
- The espionage system would have provided a non-violent alternative to raiding for
  gathering intelligence and countering alien infiltration.

## Organization Leader Interactions

A system for directly interacting with the leaders of Mega-Primus organizations was planned
but cut.

### Planned Interactions

| Action        | Planned Function                                                            |
|---------------|----------------------------------------------------------------------------|
| Tail          | Follow an organization leader to gather intelligence on their movements, meetings, and potential alien contacts. |
| Arrest        | Detain an organization leader, removing them from their position. Would have diplomatic consequences with the target organization and its allies. |
| Interrogate   | Question a detained leader to extract information about alien infiltration, organization plans, and inter-organization dealings. |
| Assassinate   | Eliminate an organization leader. Would severely damage relations but could disrupt a heavily infiltrated organization's alien-controlled leadership. |

These interactions would have provided deep strategic options for managing the
organizational web of Mega-Primus, allowing surgical interventions instead of the blunt
instrument of building raids.

## Vehicle Driving Skill

A dedicated vehicle driving skill for agents was planned but cut.

- Agents would have had a **Driving** skill that affected their performance when operating
  ground vehicles.
- Higher driving skill would have improved vehicle speed, handling, and combat effectiveness
  when the agent was assigned as a driver.
- This skill was tied to the planned expanded ground vehicle system.
- In the released game, vehicles operate automatically without agent skill modifiers.

## Swimming and Water Features

Water-based gameplay features were planned for Mega-Primus.

- Certain areas of the city were intended to have **water features** (rivers, canals,
  flooded sections).
- Agents would have had a **Swimming** ability or skill.
- Tactical missions in or near water would have required agents capable of operating in
  aquatic environments.
- This feature was likely inspired by X-COM: Terror from the Deep, the previous game in
  the series which was entirely water-themed.
- In the released game, no water terrain or swimming mechanics exist.

## Sanity Mechanic

A separate **Sanity** stat was planned, distinct from the existing morale and psionic
defense systems.

- Sanity would have been a long-term mental health stat that degraded over time based on
  combat exposure, alien encounters, and traumatic events.
- Unlike morale (which resets between missions), Sanity would have persisted and
  accumulated over an agent's career.
- Low Sanity would have caused permanent behavioral changes, reduced combat effectiveness,
  and possibly made agents unavailable for duty.
- Recovery would have required time off-duty or treatment at medical facilities.
- This mechanic would have added a long-term personnel management dimension, forcing
  players to rotate agents rather than relying on the same elite squad for every mission.
- In the released game, morale handles all mental state effects on a per-mission basis only.

## Expanded Alien Dimensions

The Alien Dimension was planned to be significantly larger and more varied than what shipped.

- **9 randomly generated alien dimensions** were originally planned, each with unique
  terrain, structures, and challenges.
- Only **3 dimensions were completed** and included in the final game.
- The remaining 6 dimensions were in various stages of development when cut.
- Random generation would have meant each playthrough featured different alien dimension
  layouts, increasing replayability.
- The released game's alien dimension, while still a living organism with multiple
  protrusions, is more limited in variety than originally envisioned.

## Multiplayer

A multiplayer mode supporting up to 8 players was planned.

- **Up to 8 players** would have been able to compete in tactical combat scenarios.
- The multiplayer was envisioned for the tactical layer only (not the strategic cityscape
  layer).
- Players would have selected squads, equipment, and starting positions, then fought in
  turn-based or real-time tactical battles.
- Network play over LAN and potentially modem connections was planned.
- The dual combat mode (real-time and turn-based) would have provided two distinct
  multiplayer experiences.
- Multiplayer was cut relatively late in development due to balancing and technical
  challenges.

## Scenario Generator

A scenario generator for creating custom tactical missions was planned.

- Players would have been able to set parameters (map type, alien composition, equipment
  restrictions, objectives) to generate custom tactical missions.
- This would have allowed replayable standalone tactical combat outside the campaign.
- The scenario generator would have been useful for testing specific tactical situations
  and for multiplayer setup.
- This feature was cut but the concept influenced later X-COM-inspired games.

## Additional Agent Skills

Several additional agent skills were planned beyond what shipped in the final game.

| Planned Skill      | Intended Function                                                      |
|--------------------|------------------------------------------------------------------------|
| Driving            | Affected ground vehicle operation performance. See Vehicle Driving Skill section above. |
| Flying             | Affected performance when using personal flight equipment (jetpacks, grav-packs). Would have influenced flight speed, maneuverability, and fuel efficiency. |
| Perceptive Ability | A dedicated perception/awareness stat. Would have affected detection of hidden units, traps, and ambushes. In the released game, detection is handled by the Reactions stat. |

These skills would have added depth to agent specialization, encouraging players to develop
agents for specific roles rather than general-purpose soldiers.

## Impact on OpenApoc

These cut features represent potential expansion opportunities for OpenApoc:

- **Espionage System**: Would add significant strategic depth. Community interest is high.
- **Organization Leader Interactions**: Could complement the existing diplomacy system.
- **Expanded Alien Dimensions**: Random generation would increase replayability.
- **Multiplayer**: Complex to implement but would significantly expand the game's appeal.
- **Additional Skills**: Relatively straightforward to add and would deepen gameplay.

Any implementation of cut features should be carefully designed to integrate with the
existing game systems and maintain balance.

## Sources

- [Cut Features (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Cut_Features_(Apocalypse))
- [Espionage (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Espionage_(Apocalypse))
- [Alien Dimension (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Alien_Dimension_(Apocalypse))
- [Multiplayer (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Multiplayer_(Apocalypse))
