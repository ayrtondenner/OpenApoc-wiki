# Research & Manufacturing (X-COM: Apocalypse)

This document covers the research and manufacturing systems in the original X-COM: Apocalypse
(1997). Research is the primary means of technological progression, and manufacturing allows
X-COM to produce advanced equipment and generate revenue.

## Research Overview

Research in X-COM: Apocalypse is split into two distinct branches, each requiring its own
type of scientist and laboratory facility. This dual-branch system forces the player to
balance investment between two parallel tech trees.

### Research Branches

| Branch           | Scientist Type        | Facility              | Focus                                        |
|------------------|-----------------------|-----------------------|----------------------------------------------|
| Biochemistry     | Biochemists           | Biochemistry Lab      | Alien biology, autopsies, toxins, biological weapons |
| Quantum Physics  | Quantum Physicists    | Quantum Physics Lab   | Alien technology, energy weapons, propulsion, dimension travel |

- Scientists of one type cannot work in the other branch's lab.
- Each branch has its own research queue.
- Research speed is proportional to the number of scientists assigned to a project.
- Advanced versions of each lab type exist, providing more workspace per facility.

## Biochemistry Research Path

The Biochemistry branch focuses on understanding alien biology and developing biological
countermeasures.

### Key Research Progression

```
Alien Autopsies (each alien species)
    |
    v
Genetic Structure Analysis
    |
    v
Toxin A --> Toxigun
    |
    v
Toxin B
    |
    v
Toxin C (most lethal)
```

### Major Biochemistry Research Topics

| Research Topic              | Prerequisites          | Unlocks                                        |
|-----------------------------|------------------------|------------------------------------------------|
| Alien Autopsies             | Alien corpse/specimen  | Information about each alien species. Required for downstream research. |
| Genetic Structure           | Multiple autopsies     | Understanding of alien biochemistry. Opens toxin research. |
| Toxin A                     | Genetic Structure      | First toxin ammo type. Mildly effective against aliens. |
| Toxin B                     | Toxin A                | Second toxin ammo type. Moderately effective.  |
| Toxin C                     | Toxin B                | Third and most lethal toxin. Devastating to organic aliens. |
| Toxigun                     | Toxin A                | The weapon platform that fires toxin projectiles. |
| Anti-Alien Gas              | Genetic Structure      | Grenade/area weapon. Lethal to aliens, harmless to humans. |
| Bio-Transport Module        | Advanced autopsies     | Allows live alien containment and transport.   |
| Advanced Biochemistry topics| Various                | Medical improvements, hybrid research, etc.    |

### Autopsy Notes

- Each alien species requires a separate autopsy research project.
- Autopsies require a specimen (dead or alive) in Alien Containment.
- Completing autopsies is essential for unlocking the Toxin research chain.
- Autopsy research also provides intelligence about alien capabilities and weaknesses,
  displayed in the UFOpaedia.

## Quantum Physics Research Path

The Quantum Physics branch focuses on alien technology, energy systems, and dimensional
travel.

### Key Research Progression

```
Alien Artifact Analysis (weapons, equipment)
    |
    +---> Alien Propulsion Systems
    |         |
    |         v
    |     Dimension Probe --> Dimension Gate Generator
    |
    +---> Alien Control Systems
    |
    +---> Alien Energy Systems
    |         |
    |         v
    |     Elerium-115 Technology
    |         |
    |         v
    |     Advanced Weapons/Armor
    |
    +---> Disruptor Weapons (Personal & Vehicle)
```

### Major Quantum Physics Research Topics

| Research Topic               | Prerequisites           | Unlocks                                       |
|------------------------------|-------------------------|-----------------------------------------------|
| Alien Artifact Analysis      | Recovered alien items   | Base understanding of alien technology.        |
| Alien Propulsion Systems     | Artifact analysis       | Understanding of UFO engines. Leads to vehicle upgrades. |
| Alien Control Systems        | Artifact analysis       | Understanding of UFO navigation and control.   |
| Alien Energy Systems         | Artifact analysis       | Understanding of Elerium-based power. Opens advanced energy tech. |
| Elerium-115                  | Energy Systems          | Fuel for advanced engines and weapons.         |
| Dimension Probe              | Propulsion + Control    | Unmanned probe vehicle for exploring alien dimension. |
| Dimension Gate Generator     | Dimension Probe research| Allows X-COM to open its own gates to the alien dimension. |
| Personal Disruptor Shield    | Energy Systems          | Equippable energy shield for agents.           |
| Disruptor Weapons            | Energy Systems          | Advanced energy weapons (Devastator Cannon, etc.). |
| Disruptor Armor              | Multiple advanced topics| Best armor in the game.                        |
| Dimension Destabilizer       | Advanced disruptor tech | Heavy area-effect disruptor weapon.            |

## Manufacturing

Manufacturing allows X-COM to produce equipment using engineers in workshop facilities.

### Manufacturing Basics

- **Engineers**: The workforce for manufacturing. Hired through the personnel market.
- **Maximum**: 50 engineers can be employed across all bases.
- **Workshops**: Standard Workshops hold a limited number of engineers.
- **Advanced Workshops**: Hold more engineers per facility and may be required for certain
  advanced items.
- **Manufacturing Queue**: Each base has its own manufacturing queue. Multiple items can be
  queued.
- **Materials**: Manufacturing requires raw materials, which may include alien artifacts,
  Elerium, and money.

### Manufacturing Facility Comparison

| Facility           | Engineer Capacity | Prerequisites               | Notes                     |
|--------------------|-------------------|-----------------------------|---------------------------|
| Workshop           | Lower             | None                        | Available from game start |
| Advanced Workshop  | Higher            | Research (Advanced Workshop) | More efficient use of base space |

### Manufacturing for Profit

Manufacturing items for sale is a viable economic strategy, especially in the mid-to-late
game when advanced items are unlocked.

| Item                    | Profit Margin | Notes                                              |
|-------------------------|---------------|----------------------------------------------------|
| Toxigun                 | High          | Relatively cheap materials, sells well. Strong profit item. |
| Personal Disruptor Shield| High         | High demand from organizations. Excellent profit.  |
| Advanced Weapons        | Moderate      | Requires alien materials but sells at premium.     |

Manufacturing for profit can supplement or even replace Senate funding as a primary income
source, especially if Senate relations deteriorate.

### Key Manufacturing Considerations

- Manufactured items that are not needed for X-COM operations can be sold on the open
  market for income.
- Some items can only be manufactured (not purchased), making the manufacturing system
  essential for endgame equipment.
- Manufacturing speed depends on the number of engineers assigned and the complexity of
  the item.
- Raw material availability can bottleneck production, especially for items requiring
  Elerium or rare alien components.

## Research Strategy Notes

### Early Game Priority

1. Begin alien autopsies immediately as specimens become available.
2. Start Quantum Physics analysis of any recovered alien artifacts.
3. Rush toward Toxin A and the Toxigun for a significant combat advantage.

### Mid Game Priority

1. Complete the Toxin B and C research for maximum biological weapon effectiveness.
2. Develop Dimension Probe technology to begin alien dimension exploration.
3. Research Personal Disruptor Shields for agent survivability.

### Late Game Priority

1. Develop Disruptor Armor for maximum agent protection.
2. Research Dimension Gate Generator for controlled access to the alien dimension.
3. Complete remaining weapon and vehicle upgrade research.

## Sources

- [Research (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Research_(Apocalypse))
- [Manufacturing (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Manufacturing_(Apocalypse))
- [Biochemistry (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Biochemistry_(Apocalypse))
- [Quantum Physics (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Quantum_Physics_(Apocalypse))
- [Toxigun (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Toxigun_(Apocalypse))
