# Scoring & Difficulty (X-COM: Apocalypse)

This document covers the scoring system, funding mechanics, difficulty levels, and dynamic
difficulty scaling in the original X-COM: Apocalypse (1997). The scoring system determines
X-COM's weekly funding, while the dynamic difficulty system adjusts the alien threat based
on player performance.

## Scoring System

X-COM's performance is evaluated through a composite score that determines weekly funding
from the Mega-Primus Senate. The score is assessed weekly.

### Score Formula

The weekly performance score is calculated as:

```
Total Score = Combat Rating
            + Leadership
            - Casualties
            + Captured Aliens
            + Captured Equipment
            - Lost Equipment
```

### Score Components

| Component           | Description                                                               |
|---------------------|---------------------------------------------------------------------------|
| Combat Rating       | Points earned from killing aliens and destroying UFOs. Each alien species and UFO type has a specific point value. |
| Leadership          | Bonus based on the number of agents successfully deployed and missions completed. |
| Casualties          | Penalty for X-COM agents killed or permanently lost during the week.      |
| Captured Aliens     | Bonus for live aliens captured and brought to Alien Containment.          |
| Captured Equipment  | Bonus for alien equipment recovered from tactical missions.               |
| Lost Equipment      | Penalty for X-COM equipment lost or destroyed during missions.            |

### Score Penalties

Several events impose direct score penalties:

| Event                     | Penalty                                                              |
|---------------------------|----------------------------------------------------------------------|
| Alien Alert (unaddressed) | **-30 points per alert**. When an alien incursion occurs and X-COM fails to respond or fails the mission, a penalty is applied. |
| Escaped UFO               | **-1/4 of the UFO's score value**. If a UFO escapes without being shot down or driven off, X-COM loses a quarter of the points that UFO was worth. |
| City Block Destruction    | Significant penalty when buildings are destroyed, whether by aliens or X-COM collateral damage. |

## Weekly Funding

X-COM receives funding from the Mega-Primus Senate on a weekly cycle.

- **Assessment Day**: Funding is assessed every **Monday at midnight** (game time).
- **Funding Amount**: Determined by the weekly performance score and the Senate's
  relationship with X-COM.
- **Senate Relationship**: A positive Senate relationship increases the funding multiplier.
  A hostile Senate may reduce funding to near-zero, threatening X-COM's financial viability.
- **Minimum Funding**: Even with poor performance, X-COM receives some baseline funding
  unless the Senate has turned completely hostile.

### Funding Risks

- If X-COM's score consistently drops, the Senate reduces funding.
- If the Senate becomes infiltrated by aliens, funding may be cut regardless of X-COM's
  performance.
- Manufacturing for profit (see [research-manufacturing.md](research-manufacturing.md)) can
  supplement or replace Senate funding if relations deteriorate.

## Difficulty Levels

The game offers five difficulty levels, selected at the start of a new campaign. Difficulty
affects starting conditions, alien strength, and the pace of escalation.

| Difficulty | Description                                                                   |
|------------|-------------------------------------------------------------------------------|
| Novice     | Easiest setting. Reduced alien numbers, weaker aliens, more starting resources. Good for learning the game systems. |
| Easy       | Below-average difficulty. Fewer aliens and slower escalation than normal.      |
| Medium     | Standard difficulty. Balanced alien numbers, escalation rate, and resource availability. Intended experience. |
| Hard       | Above-average difficulty. More aliens, faster escalation, tougher opponents.   |
| Superhuman | Maximum difficulty. Most aliens, fastest escalation, strongest opponents, fewest resources. Intended for expert players. |

### Difficulty Effects

Higher difficulty levels affect multiple game systems:

- **Alien Numbers**: More aliens spawn per mission at higher difficulties.
- **Alien Stats**: Alien health, accuracy, and other stats scale upward.
- **Starting Resources**: X-COM receives fewer starting funds, agents, and equipment at
  higher difficulties.
- **Escalation Rate**: The alien invasion progresses faster, introducing tougher UFOs and
  alien types earlier.
- **Infiltration Speed**: Alien infiltration of organizations proceeds faster at higher
  difficulties.

## Dynamic Difficulty

Beyond the static difficulty setting, X-COM: Apocalypse features a **dynamic difficulty
system** that adjusts the alien threat based on ongoing player performance. This system
operates on two axes.

### Tactical Performance Affects Alien Equipment

- The aliens' equipment quality in tactical missions is influenced by X-COM's tactical
  combat score.
- **Performing well in tactical combat** causes aliens to bring better equipment to
  subsequent missions: upgraded weapons, more armor, and more dangerous alien types.
- **Performing poorly** results in aliens using weaker loadouts.
- This creates a natural balancing mechanism: skilled players face tougher opponents, while
  struggling players face slightly easier missions.

### Cityscape Performance Affects UFO Technology

- X-COM's performance in the cityscape layer (shooting down UFOs, responding to incidents)
  influences the technology level of incoming UFOs.
- **Strong cityscape performance** causes the aliens to deploy more advanced UFO types
  earlier in the campaign.
- **Weak cityscape performance** slows the progression of UFO types.
- This means that an X-COM force that dominates the skies early will face Battleships and
  Motherships sooner than one that struggles with basic interceptions.

### Organization Tech Level Progression

- **Organizations upgrade their Tech Level by +1 weekly**, independently of player actions.
- This means that even without alien interference, the organizations of Mega-Primus
  gradually acquire better technology, vehicles, and equipment.
- This affects what is available for purchase from organizations and the strength of
  organization forces if they become hostile.
- The weekly tech level increase is automatic and cannot be prevented or accelerated by
  the player.

### Dynamic Difficulty Implications

The dynamic difficulty system means that:

1. **There is no optimal "farming" strategy**: Crushing every mission drives up difficulty,
   while intentionally losing is penalized by score reductions and funding cuts.
2. **The game adapts**: Players who excel at tactical combat but neglect the cityscape (or
   vice versa) will find the neglected axis becoming more challenging as the other remains
   manageable.
3. **Late-game difficulty is partly player-driven**: Two campaigns on the same static
   difficulty setting can feel very different in the late game depending on how the player
   performed throughout.

## Sources

- [Score (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Score_(Apocalypse))
- [Funding (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Funding_(Apocalypse))
- [Difficulty (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Difficulty_(Apocalypse))
- [Dynamic Difficulty (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Dynamic_Difficulty_(Apocalypse))
