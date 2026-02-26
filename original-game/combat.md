# Combat System (X-COM: Apocalypse)

This document covers the tactical combat mechanics of the original X-COM: Apocalypse (1997)
as a reference for OpenApoc development. The game features a unique dual-mode combat system,
a wide variety of damage types, and layered equipment progression from early human weapons
through alien-derived technology.

## Combat Modes

X-COM: Apocalypse is the first game in the series to offer two distinct combat modes. The
player selects the mode before each tactical mission. Both modes use the same maps and unit
stats, but play very differently in practice.

### Turn-Based Mode

Turn-based combat follows the traditional X-COM model. Each side takes turns, and agents
spend Time Units (TUs) to perform actions.

- **Time Units (TU)**: Each agent receives TUs at the start of their turn based on the
  Speed stat. All actions (movement, firing, turning, picking up items) cost TUs.
- **Reaction Fire**: If an agent has remaining TUs at the end of their turn, they may
  automatically fire at enemies that move within their field of view during the alien turn.
  Reaction fire chance depends on the Reactions stat and remaining TUs.
- **Psionic Effects**: Stun, panic, and mind control effects from psionic attacks last
  exactly one turn, making psionics less dominant than in real-time.
- **Security Station Turret Bug**: In turn-based mode, Security Station turrets at X-COM
  bases have a TU allocation bug that can cause them to malfunction or fail to fire properly.
  See [known-bugs.md](known-bugs.md) for details.

### Real-Time Mode

Real-time combat runs continuously, with the player issuing orders while the game is active.
The player can pause at any time to issue orders.

- **Simultaneous Movement**: All units (X-COM and alien) move and act at the same time.
  Speed stat directly determines movement rate.
- **Continuous Psi Drain**: Psionic attacks drain psi-energy continuously rather than in
  discrete per-turn chunks, making psi attacks more resource-intensive but also more
  immediately impactful.
- **Weaker Alien AI**: In real-time mode, alien AI tends to be less tactically sophisticated.
  Aliens frequently charge in straight lines toward X-COM agents rather than using cover or
  flanking maneuvers. This makes real-time mode generally easier for experienced players.
- **Auto-Fire Dominance**: Weapons with high rates of fire become disproportionately strong
  in real-time since agents fire continuously without TU constraints.

## Damage Types

X-COM: Apocalypse features a significantly expanded damage model compared to earlier games.
Each damage type interacts differently with armor and shields.

| Damage Type      | Description                                                                                          |
|------------------|------------------------------------------------------------------------------------------------------|
| AP (Armor Piercing) | Standard kinetic damage from conventional ballistic weapons. Effective against lightly armored targets. |
| Explosive        | Area-of-effect blast damage. Damages terrain and can destroy cover. Reduced by armor.                |
| Incendiary       | Sets targets and terrain on fire. Causes ongoing burning damage over time. Fire spreads to adjacent tiles. |
| Laser            | Energy beam damage. High accuracy, no projectile travel time. Moderate armor penetration.            |
| Plasma           | Superheated plasma bolts. High damage output, good armor penetration. Primary alien weapon type.     |
| Disruptor        | Advanced alien energy damage. Extremely high damage, excellent armor penetration. Endgame alien and X-COM weapon type. |
| Stun             | Non-lethal damage applied to the stun health pool. When stun damage exceeds remaining health, the target is knocked unconscious. Does not kill. |
| Smoke            | Obscures vision. No direct damage but blocks line of sight. Useful tactically for cover.             |
| Toxin            | Biological poison damage (Toxigun). Three variants (A, B, C) with escalating lethality. Only affects organic targets. |
| Entropy Enzyme   | Alien biological weapon. Corrodes and degrades equipment and armor on contact.                       |
| Acid Spit        | Ranged alien biological attack (Spitter aliens). Causes acid burns and equipment degradation.        |

## Personal Disruptor Shields

Personal Disruptor Shields are equippable defensive devices that absorb incoming damage before
it reaches the agent's armor and health. They are a critical piece of late-game equipment.

**Protects against:** AP, Explosive, Incendiary, Laser, Plasma, Disruptor damage types.

**Does NOT protect against:**
- Brainsuckers (bypass shields entirely)
- Smoke
- Stun Gas
- Toxigun projectiles
- Psionic attacks
- Anti-Alien Gas

The shield has a finite energy pool that depletes as it absorbs damage. Once drained, damage
passes through to the agent's armor and health normally. Shields recharge slowly over time
when not taking damage.

## Weapon Categories

### Early Human Weapons

These are the weapons available at the start of the game, purchased from Mega-Primus
organizations.

| Weapon          | Damage Type | Notes                                                        |
|-----------------|-------------|--------------------------------------------------------------|
| Lawpistol       | AP          | Standard sidearm. Low damage, fast rate of fire.             |
| Machine Gun     | AP          | Moderate damage, high ammo capacity. Good general-purpose weapon. |
| Auto Cannon     | AP/Explosive/Incendiary | Heavy weapon with three ammo types. High damage but heavy and slow. |
| Megapol Laser Pistol | Laser  | Energy sidearm. No ammo needed (battery-based).             |
| Megapol Laser Gun | Laser     | Energy rifle. Good accuracy and damage, battery-based.       |

### Advanced Human Weapons

Unlocked through research or available from certain organizations.

| Weapon               | Damage Type | Notes                                                   |
|----------------------|-------------|---------------------------------------------------------|
| Toxigun              | Toxin       | Fires biological toxin rounds. Three ammo types (A, B, C) of escalating lethality. Extremely effective against organic aliens. Bypasses Disruptor Shields. |
| Devastator Cannon    | Disruptor   | Heavy human-manufactured disruptor weapon. High damage but heavy and expensive. |
| Dimension Destabilizer | Disruptor | Alien-derived heavy weapon. Area effect disruptor damage. |

### Toxigun vs Devastator Endgame Meta

The Toxigun and Devastator Cannon represent two competing endgame strategies:

- **Toxigun**: Cheaper, lighter, bypasses shields, highly effective against organic aliens.
  Toxin C is lethal to virtually all organic life forms. Useless against robotic enemies and
  Androids. The three ammo types (A, B, C) correspond to research progress, with C being the
  most potent.
- **Devastator Cannon**: Expensive and heavy, but deals universal disruptor damage that
  works against all targets regardless of organic/inorganic status. Better for mixed enemy
  compositions.

Most experienced players favor a Toxigun-heavy loadout for organic alien missions, with
Devastator Cannons reserved for situations where universal damage is needed.

### Mind Bender

The Mind Bender is a special weapon used for psionic attacks. See [psionics.md](psionics.md)
for full details.

## Armor

| Armor Type            | Protection Level | Notes                                                   |
|-----------------------|------------------|---------------------------------------------------------|
| Megapol Armor         | Low              | Starting armor. Cheap and readily available.            |
| Marsec Armor          | Medium           | Better protection than Megapol. Available from Marsec.  |
| X-COM Disruptor Armor | High             | Best armor in the game. Requires research and manufacturing. Provides excellent protection against all damage types. |

Armor provides directional protection (front, sides, back, top, bottom), with the front
typically offering the highest armor value. Damage that exceeds the armor value for the hit
location passes through to the agent's health.

## Sources

- [Apocalypse - UFOpaedia](https://www.ufopaedia.org/index.php?title=Apocalypse)
- [Equipment (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Equipment_(Apocalypse))
- [Damage (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Damage_(Apocalypse))
- [Weapons (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Weapons_(Apocalypse))
- [Armor (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Armor_(Apocalypse))
- [Personal Disruptor Shield - UFOpaedia](https://www.ufopaedia.org/index.php?title=Personal_Disruptor_Shield)
