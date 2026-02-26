# Aliens (X-COM: Apocalypse)

This document covers the alien species, ecology, and dimension in the original X-COM:
Apocalypse (1997). The alien threat in Apocalypse is significantly different from previous
X-COM games, featuring a complex alien ecosystem with lifecycle stages, specialized roles,
and a living alien dimension.

## Alien Species

X-COM: Apocalypse features 14 distinct alien types. Unlike previous games where aliens were
primarily humanoid soldiers, Apocalypse's aliens form a complete ecosystem with predators,
parasites, and metamorphosing organisms.

### Infiltration and Parasitic Aliens

| Alien       | HP  | Role | Description                                                                     |
|-------------|-----|------|---------------------------------------------------------------------------------|
| Micronoid   | --  | Infiltrator | Microscopic alien organisms. Cannot be encountered in tactical combat. Spread through People Tubes to infiltrate organizations. The invisible strategic threat driving the infiltration mechanic. |
| Brainsucker | Low | Parasite | Small, fast creature launched from Brainsucker Pods. Leaps at agents and attaches to their head, taking permanent mind control. Bypasses Personal Disruptor Shields. Cannot attack prone units (bug). Neutralized only by killing it before it reaches the target or killing the controlled host. |
| Alien Egg   | Low | Spawner | Immobile organic structure that hatches Multiworms. Found in alien buildings and dimension. Destroying eggs prevents further alien spawning in an area. |

### Metamorphosing Aliens (Lifecycle Chain)

These aliens form the core of the alien ecology lifecycle, with each stage capable of
developing into a higher form.

| Alien       | HP     | Role     | Description                                                              |
|-------------|--------|----------|--------------------------------------------------------------------------|
| Multiworm   | High   | Assault  | Large worm-like creature. Tough and aggressive. When killed, splits into four Hyperworms. Must be fully destroyed to prevent spawning. |
| Hyperworm   | Low    | Swarm    | Small worm spawned from dead Multiworms (4 per Multiworm). Individually weak but dangerous in numbers. Can metamorphose into a Chrysalis. |
| Chrysalis   | Medium | Cocoon   | Immobile metamorphosing stage. A Hyperworm that has cocooned itself. If left undisturbed, transforms into a higher alien form (Anthropod, Skeletoid, Spitter, or Megaspawn). High priority target -- destroy before metamorphosis completes. |

### Combat Aliens

| Alien       | HP     | Role        | Description                                                          |
|-------------|--------|-------------|----------------------------------------------------------------------|
| Anthropod   | Medium | Infantry    | Humanoid alien soldier. The most common combat alien. Carries weapons (plasma-based). Some variants have psionic ability. Versatile and dangerous in groups. |
| Skeletoid   | Medium | Infantry    | Skeletal humanoid alien. Similar combat role to Anthropods but with different stat distributions. Carries alien weapons. |
| Spitter     | Medium | Ranged      | Alien with biological ranged attack (Acid Spit). Attacks cause acid damage and equipment degradation. In the original game, Spitter AI is bugged and often passive (see [known-bugs.md](known-bugs.md)). |
| Popper      | Low    | Suicide     | Unstable alien that detonates on contact or when killed. Deals heavy explosive damage in a radius. Extremely dangerous in confined spaces. Prioritize killing at range before they close distance. |
| Megaspawn   | Very High | Heavy    | Massive alien heavy unit. Extremely durable with devastating attacks. The toughest standard combat alien. Slow but can absorb enormous punishment. In the original game, has a retreat behavior bug (see [known-bugs.md](known-bugs.md)). |

### Psionic and Command Aliens

| Alien       | HP     | Role      | Description                                                            |
|-------------|--------|-----------|------------------------------------------------------------------------|
| Psimorph    | High   | Psionic   | Powerful psionic alien. Capable of devastating mind control, panic, and stun attacks at long range. Floats and can move through obstacles. The most dangerous psionic threat on the battlefield. High priority target. |
| Queenspawn  | Very High | Boss   | Alien queen. Found in the alien dimension. Extremely tough and dangerous. Killing Queenspawns is necessary to damage the alien dimension's capacity to wage war. |

## Alien Ecology Lifecycle

One of Apocalypse's unique features is the alien metamorphosis lifecycle. Aliens are not
simply manufactured; they grow and evolve through stages.

### Lifecycle Diagram

```
Alien Egg
    |
    v
Multiworm (when killed, splits into 4 Hyperworms)
    |
    v
Hyperworm (can enter cocoon phase)
    |
    v
Chrysalis (immobile metamorphosis stage)
    |
    +--> Anthropod
    +--> Skeletoid
    +--> Spitter
    +--> Megaspawn
```

### Lifecycle Details

1. **Alien Eggs** are placed by the aliens in buildings they control and throughout the
   alien dimension. Eggs periodically hatch into Multiworms.

2. **Multiworms** are large, aggressive worm creatures. When a Multiworm is killed, its
   body splits into **four Hyperworms**. This means killing a Multiworm actually increases
   the number of enemies temporarily.

3. **Hyperworms** are small and individually weak. If left alive long enough, a Hyperworm
   enters a **Chrysalis** stage, becoming immobile while it metamorphoses.

4. **Chrysalis** is the cocoon stage. If undisturbed, the Chrysalis hatches into a higher
   alien form. The resulting alien type depends on conditions, but can be any of the combat
   aliens: Anthropod, Skeletoid, Spitter, or Megaspawn.

5. This lifecycle means that leaving aliens alive or failing to clear an area completely
   can result in more and more dangerous aliens appearing over time. Chrysalises should be
   destroyed immediately when spotted.

### Tactical Implications

- **Multiworm kills are not clean kills**: Always be prepared for the four Hyperworms that
  spawn from a dead Multiworm. Position agents to handle the swarm.
- **Chrysalis priority**: Destroy Chrysalises before they complete metamorphosis. A Chrysalis
  becoming a Megaspawn in the middle of a tactical mission is a serious threat.
- **Egg destruction**: Clear alien eggs from buildings to prevent ongoing spawning.
- **Containment**: Live aliens of any lifecycle stage can be captured for research, but
  Multiworms and higher forms are difficult to stun.

## Brainsucker Mechanics

Brainsuckers deserve special attention due to their unique and dangerous mechanics:

- **Deployment**: Brainsuckers are launched from Brainsucker Pods carried by other aliens
  (typically Anthropods). The pod has limited ammunition.
- **Attack**: The Brainsucker leaps at a target agent. If it reaches the agent's head, it
  attaches permanently and takes control of the agent.
- **Mind Control**: A Brainsuckered agent is permanently lost. They fight for the aliens for
  the rest of the mission. The only way to recover is to kill the controlled agent.
- **Counters**: Shoot the Brainsucker mid-leap, use agents with helmets (provides some
  protection), or position Androids (immune to Brainsuckers) as front-line screens.
- **Shield Bypass**: Brainsuckers bypass Personal Disruptor Shields entirely.
- **Prone Bug**: Brainsuckers cannot attack prone (lying down) units in the original game.
  This is a known bug, not intended behavior.

## The Alien Dimension

The Alien Dimension is the extraterrestrial realm from which the alien invasion originates.
It is not a planet but a living organism.

### Structure

The Alien Dimension is a massive living entity with **10 protrusions** (organic structures)
that serve different functions:

- Each protrusion contains alien structures, organisms, and defenses.
- The terrain is organic and alien, with floors, walls, and features made of living tissue.
- Navigation is non-intuitive compared to human buildings.

### Accessing the Alien Dimension

1. **Dimensional Gates**: Aliens open Dimensional Gates in Mega-Primus airspace to send
   UFOs through. These gates can also be used by X-COM vehicles equipped with Dimension
   Shift technology.
2. **Dimension Probe**: The first X-COM vehicle capable of entering the alien dimension.
   Used for reconnaissance.
3. **Dimension Gate Generator**: Researched technology that allows X-COM to open its own
   gates on demand, rather than relying on alien-created gates.

### Alien Dimension Missions

- Missions in the alien dimension are tactical combat missions within the organic alien
  structures.
- X-COM must systematically destroy the alien dimension's key structures to weaken and
  ultimately defeat the alien invasion.
- The final missions of the game take place in the alien dimension, culminating in the
  destruction of the alien command structure.

## Sources

- [Aliens (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Aliens_(Apocalypse))
- [Alien Life Cycle (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Alien_Life_Cycle_(Apocalypse))
- [Brainsucker (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Brainsucker_(Apocalypse))
- [Alien Dimension (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Alien_Dimension_(Apocalypse))
- [Multiworm (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Multiworm_(Apocalypse))
