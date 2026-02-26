# Agents (X-COM: Apocalypse)

This document covers the agent system in the original X-COM: Apocalypse (1997). Agents
are the individual soldiers, scientists, engineers, and operatives that X-COM employs.
The game features three distinct agent species, a comprehensive stat system, and multiple
training and improvement paths.

## Agent Stats

Each agent has a set of stats that determine their effectiveness in combat and other roles.

| Stat         | Description                                                                           | Range  |
|--------------|---------------------------------------------------------------------------------------|--------|
| Health       | Total hit points. When reduced to zero, the agent dies.                               | 1-100  |
| Accuracy     | Determines chance to hit with ranged weapons. Higher is better.                       | 1-100  |
| Reactions    | Determines reaction fire speed (turn-based) and general responsiveness (real-time).   | 1-100  |
| Speed        | Determines movement rate and TU allocation in turn-based mode.                        | 1-100  |
| Stamina      | Determines how long an agent can run/act before becoming fatigued.                    | 1-100  |
| Strength     | Determines carrying capacity and resistance to certain physical effects.              | 1-100  |
| Bravery      | Determines resistance to morale loss from casualties, psionic attacks, and fear.      | 10-100 |
| Psi-Energy   | Maximum psionic energy pool. Powers psionic attacks via the Mind Bender.              | 0-100  |
| Psi-Attack   | Offensive psionic power. Zero means the agent cannot use psionics offensively.        | 0-100  |
| Psi-Defence  | Defensive resistance to enemy psionic attacks.                                        | 0-100  |

Bravery is always a multiple of 10 (10, 20, 30, ..., 100) and does not improve through
training or combat experience.

## Agent Types

X-COM: Apocalypse introduces three distinct agent species, each with unique strengths and
limitations.

### Humans

Humans are the most versatile agent type and form the core of most X-COM squads.

- **Physical Stats**: Average starting values across all physical stats. Wide variance
  between recruits.
- **Psi Stats**: Random. Some humans have latent psionic ability (non-zero Psi-Attack),
  while others have none. All humans have some Psi-Defence.
- **Improvement**: All stats can improve through combat experience and base training
  facilities. Humans have the highest overall growth potential.
- **Vulnerabilities**: Susceptible to Brainsuckers (can be mind-controlled by implantation),
  psionic attacks, toxins, and all conventional threats.

### Hybrids

Hybrids are human-alien crossbreeds with a predisposition toward psionic ability. They are
recruited through the Mutant Alliance organization.

- **Physical Stats**: Below average. Lower Health, Strength, Speed, and Stamina than
  comparable Humans. Fragile in direct combat.
- **Psi Stats**: Significantly above average. High starting Psi-Attack, Psi-Defence, and
  Psi-Energy. Best natural psionics of any playable agent type.
- **Improvement**: All stats can improve, though physical stats improve slowly and from a
  lower base. Psi stats improve quickly.
- **Role**: Dedicated psionic operatives. Best used in rear-echelon positions using Mind
  Benders, with Human or Android agents providing physical security.
- **Vulnerabilities**: Susceptible to Brainsuckers, psionic attacks (though high Psi-Defence
  helps), and all physical threats. Their low Health makes them fragile.

### Androids

Androids are synthetic humanoid agents. They are manufactured, not recruited, and have
fundamentally different characteristics from biological agents.

- **Physical Stats**: Superior. High starting Health, Accuracy, Reactions, Speed, Strength,
  and Stamina. Excellent baseline combat capability.
- **Psi Stats**: Zero across the board. Androids have no psionic ability whatsoever.
- **Improvement**: **Androids CANNOT improve any stats.** Their starting stats are their
  permanent stats. They do not gain experience from combat and do not benefit from training
  facilities.
- **Psi Immunity**: Androids are completely immune to all psionic attacks. They cannot be
  panicked, stunned via psionics, or mind controlled. This makes them invaluable against
  psionic-heavy alien forces.
- **Brainsucker Immunity**: Brainsuckers cannot implant Androids. This removes a major
  tactical threat.
- **Vulnerabilities**: No psionic defense means no psionic offense; cannot use Mind Benders.
  Despite high stats, their inability to improve means they fall behind experienced Human
  agents in the late game.

## Stat Comparison by Agent Type

| Stat         | Human (Average) | Hybrid (Average) | Android (Fixed) |
|--------------|-----------------|-------------------|-----------------|
| Health       | 40-60           | 25-40             | 55-70           |
| Accuracy     | 40-60           | 30-50             | 60-75           |
| Reactions    | 40-60           | 30-50             | 55-70           |
| Speed        | 50-70           | 40-55             | 60-75           |
| Stamina      | 40-60           | 30-45             | 55-70           |
| Strength     | 40-60           | 25-40             | 60-75           |
| Bravery      | 10-100          | 10-80             | 100             |
| Psi-Energy   | 0-60            | 40-80             | 0               |
| Psi-Attack   | 0-50            | 30-70             | 0               |
| Psi-Defence  | 20-60           | 40-80             | N/A (Immune)    |

Note: These are approximate ranges for newly recruited agents. Actual values vary per
individual.

## Training and Improvement

### Combat Experience

Agents improve stats by using them in combat:

- Firing weapons improves Accuracy.
- Being shot at and surviving improves Reactions (in some contexts) and Bravery indirectly
  through morale management.
- Moving in combat improves Speed and Stamina.
- Carrying heavy loads improves Strength.
- Using psionics improves Psi-Attack, Psi-Defence, and Psi-Energy.

### Base Training Facilities

| Facility      | Stats Trained                           | Notes                              |
|---------------|-----------------------------------------|------------------------------------|
| Training Area | Strength, Reactions, Stamina, Health    | General physical conditioning. Agents assigned here train passively over time. |
| Psi-Gym       | Psi-Attack, Psi-Defence, Psi-Energy    | Psionic training. Only effective for agents with existing psionic ability (non-zero Psi-Attack). |

- Training is slower than combat improvement but is safe and consistent.
- Agents can be assigned to training facilities from the base management screen.
- Androids gain no benefit from any training facility.

## Morale System

Agent morale affects combat performance and can cause loss of control.

### Morale Factors

- **Bravery**: The primary stat governing morale resilience. Higher Bravery means slower
  morale loss and faster recovery.
- **Friendly casualties**: Seeing allied agents killed or incapacitated reduces morale.
- **Psionic attacks**: Demoralize attacks directly reduce morale.
- **Wound severity**: Taking heavy damage reduces morale.
- **Successful actions**: Killing enemies and completing objectives slightly restores morale.

### Morale States

| State    | Effect                                                                          |
|----------|---------------------------------------------------------------------------------|
| Normal   | Agent operates normally under player control.                                   |
| Panic    | Agent drops weapon and flees uncontrollably. Cannot be given orders. Recovers after a short time (turn-based: several turns; real-time: several seconds). |
| Berserk  | Agent attacks all nearby units randomly, including allies. Extremely dangerous. Cannot be controlled. Recovers unpredictably. |

## Agent Capacity

- X-COM can employ a **maximum of 100 agents** across all bases combined.
- This limit includes all agent types (Humans, Hybrids, Androids) and all roles (soldiers,
  scientists, engineers).
- Managing this cap is important in the mid-to-late game when expanding operations across
  multiple bases.

## Community Research

The following information has been gathered from OpenApoc Discord community research,
including reverse engineering, testing, and gameplay analysis.

### Android Stat Growth Correction

Contrary to the commonly stated claim that Androids cannot improve any stats, community
testing has revealed that **Androids do gain experience**, but at a **significantly slower
rate** than humans or hybrids. All stats can improve except Stamina. The improvement is so
slow that it is practically negligible in a normal campaign, which is likely why it was
originally reported as non-existent.

### Training and Healing Facility Efficiency

According to community research, training and healing facility utilization has a
non-linear efficiency curve:

- **80% utilization** is actually **more efficient per agent** than 100% capacity.
- **100% utilization** is significantly better than overloading the facility.
- **120% overwork** (exceeding capacity) causes a sharp efficiency drop and is much worse
  than operating at or below capacity.
- The rate of training/healing is internally tied to the **TPS (ticks per second) value**
  with additional modifiers based on facility type and agent stats.

Players should aim for approximately 80% capacity for optimal per-agent improvement rates.

### Engineer Hard Cap

There is a **hard cap of 50 engineers per manufacturing category** in the original game.
Assigning more than 50 engineers to a single production line provides no additional benefit.
This cap is per category, not per base.

### Scientist Travel Mechanics

According to community research, **scientists travel on foot through People Tubes** to reach
their assigned laboratories. This has an important diplomatic consequence:

- If X-COM's relationship with **Transtellar** (the People Tube operator) becomes hostile,
  scientists may be **unable to reach the base** or experience significant travel delays.
- This can effectively shut down research operations even if the scientists are technically
  employed and assigned.

### Commander Rank Requirements

According to community testing, the **Commander rank** for agents is not simply a function of
experience points. It requires:

- A **mission count threshold** -- the agent must have participated in a minimum number of
  missions.
- **Diverse mission activities** -- the agent must have performed a variety of actions across
  missions (kills, captures, recoveries, etc.), not just repeated the same activity.

This means that agents who are deployed repeatedly but perform narrow roles may never reach
Commander rank despite high mission counts.

## Sources

- [Agents (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Agents_(Apocalypse))
- [Agent Stats (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Agent_Stats_(Apocalypse))
- [Agent Types (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Agent_Types_(Apocalypse))
- [Training (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Training_(Apocalypse))
