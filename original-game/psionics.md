# Psionics (X-COM: Apocalypse)

This document covers the psionic combat system in the original X-COM: Apocalypse (1997).
Psionics is a secondary combat mechanic that allows agents (and certain aliens) to attack
enemy minds directly, bypassing armor and shields entirely. The system differs significantly
between real-time and turn-based modes.

## The Mind Bender

The Mind Bender is the sole psionic weapon in the game. It is a hand-held device that must be
equipped in an agent's hand slot to use. The Mind Bender has no ammunition but requires the
wielder to have Psi-Energy to power attacks.

- **Weight**: Light enough to carry alongside other equipment.
- **Range**: Requires line of sight to the target; effective range covers most tactical map
  distances.
- **Requirement**: The wielding agent must have a non-zero Psi-Attack stat. Agents with
  zero Psi-Attack cannot use the Mind Bender at all.

## Psi-Energy

Psi-Energy is the resource pool that fuels all psionic attacks. It functions similarly to
ammunition for conventional weapons.

- Each agent has a maximum Psi-Energy value determined by their stats.
- Psionic attacks consume Psi-Energy from the attacker's pool.
- Psi-Energy recharges slowly over time during a mission. The recharge rate is gradual and
  cannot sustain continuous high-frequency attacks.
- Once an agent's Psi-Energy is fully depleted, they cannot perform any psionic attacks until
  it partially recharges.
- Psi-Energy is fully restored between missions.

## Psionic Attack Types

The Mind Bender offers three distinct attack modes, each with different tactical applications:

### Stun

- **Effect**: Deals stun damage directly to the target's stun health pool, bypassing armor
  and shields.
- **Result**: If stun damage exceeds the target's remaining health, the target falls
  unconscious.
- **Use Case**: Non-lethal incapacitation. Useful for capturing aliens alive for research.
- **Cost**: Moderate Psi-Energy drain.

### Demoralize (Panic)

- **Effect**: Reduces the target's morale, potentially causing them to panic.
- **Result**: A panicked unit drops their weapon and flees uncontrollably. Panicked agents
  cannot be given orders until they recover. Severe morale loss can cause a unit to go
  berserk, attacking friends and foes randomly.
- **Use Case**: Disrupting dangerous enemies, forcing them to drop weapons and break
  formation.
- **Cost**: Lower Psi-Energy drain than other attack types.

### Mind Control

- **Effect**: Attempts to seize complete control of the target unit.
- **Result**: If successful, the target comes under the attacker's control for the duration
  of the effect. The controlled unit can be ordered to move, fire, drop equipment, or any
  other action as if it were a friendly unit.
- **Use Case**: Turning powerful enemies against their allies, or moving enemy units into
  disadvantageous positions.
- **Cost**: Highest Psi-Energy drain. Maintaining mind control is an ongoing cost.
- **Risk**: If the controlling agent is killed or knocked unconscious, control is broken
  immediately.

## Success Factors

The success of a psionic attack depends on several factors:

| Factor              | Role                                                                       |
|---------------------|---------------------------------------------------------------------------|
| Attacker Psi-Attack | Higher values increase the chance of a successful attack.                 |
| Defender Psi-Defence | Higher values decrease the chance of the attack succeeding.              |
| Attacker Psi-Energy | More remaining energy increases attack strength. Low energy weakens attacks. |
| Attack Type         | Stun is easiest to land; Mind Control is the hardest.                     |
| Distance            | Greater distance slightly reduces success chance.                         |

## Differences Between Real-Time and Turn-Based

The psionic system behaves differently depending on the combat mode:

### Turn-Based Mode

- Psionic attacks cost TUs to perform, like any other action.
- **Effects last exactly one turn**: A stunned or panicked unit recovers at the start of
  their next turn (assuming the effect is not re-applied). Mind control lasts until the
  start of the controlled unit's next turn.
- Psi-Energy cost is deducted as a lump sum per attack.
- This makes psionics relatively weaker in turn-based mode, as the effects are temporary
  and must be continuously re-applied.

### Real-Time Mode

- Psionic attacks are initiated and then sustained continuously.
- **Continuous Psi-Energy drain**: The attacker's Psi-Energy drains steadily while
  maintaining an effect. This means long-duration mind control or sustained stun attacks
  can quickly exhaust the attacker's reserves.
- Effects persist as long as the attack is maintained and the attacker has sufficient
  Psi-Energy.
- Mind control in particular is more powerful in real-time because there is no automatic
  "end of turn" release; the enemy remains controlled until the attacker runs out of energy,
  loses line of sight, or is incapacitated.

## Latent Psionic Ability

Not all agents have psionic capability. Whether an agent can use psionics depends on their
innate stats:

- **Psi-Attack**: Determines offensive psionic power. Agents with Psi-Attack of 0 cannot
  use the Mind Bender at all.
- **Psi-Defence**: Determines resistance to enemy psionic attacks. All agents have some
  Psi-Defence, even those with no Psi-Attack.
- **Humans**: May or may not have psionic ability. Recruits have random psi stats. Psi
  stats can be trained at the Psi-Gym.
- **Hybrids**: Naturally strong psionic ability. Start with high Psi-Attack and Psi-Defence
  values.
- **Androids**: Completely immune to psionic attacks (both as attacker and defender). Cannot
  use the Mind Bender and cannot be targeted by psionic attacks.

## Psionic Training

Agents can improve their psionic stats over time:

- The **Psi-Gym** facility at X-COM bases allows agents to train their Psi-Attack,
  Psi-Defence, and Psi-Energy stats.
- Training is slow but steady, and is the only reliable way to improve psi stats outside of
  combat.
- Using psionic attacks in combat also provides experience gains to psi stats.
- Androids cannot train psi stats (they are inherently psi-null).

## Alien Psionics

Several alien species possess psionic abilities:

- **Psimorphs**: The most powerful psionic aliens. Capable of devastating mind control and
  panic attacks. High priority targets in tactical combat.
- **Anthropods**: Some variants possess moderate psionic ability.
- **Micronoids**: The infiltrating alien organism; their psionic influence drives the
  organization infiltration mechanic at the strategic level.

When aliens use psionics against X-COM agents, the same success formula applies in reverse.
Agents with high Psi-Defence and Bravery are more resistant to alien psionic attacks.

## Sources

- [Mind Bender - UFOpaedia](https://www.ufopaedia.org/index.php?title=Mind_Bender_(Apocalypse))
- [Psionic (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Psionic_(Apocalypse))
- [Agents (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Agents_(Apocalypse))
