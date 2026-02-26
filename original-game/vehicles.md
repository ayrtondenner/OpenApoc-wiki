# Vehicles (X-COM: Apocalypse)

This document covers the vehicle system in the original X-COM: Apocalypse (1997). Vehicles
are used for cityscape combat (intercepting UFOs), transporting agents to tactical missions,
and exploring the alien dimension. The game features both air and ground vehicles, with
X-COM relying primarily on air vehicles for rapid response.

## X-COM Vehicles

X-COM can purchase and deploy several vehicle types. Vehicles are stored in base hangars
and can be equipped with weapons and engines.

| Vehicle          | Cost   | Speed         | HP  | Passengers | Weapon Slots | Notes                                                    |
|------------------|--------|---------------|-----|------------|--------------|----------------------------------------------------------|
| Hoverbike        | $5,000 | Engine + 4    | 25  | 1          | 1            | Cheapest and fastest scout. Extremely fragile. No cargo space. Best used for rapid interception of small UFOs. |
| Phoenix Hovercar | $12,000| Engine + 2    | 70  | 4          | 1            | Light transport. Decent speed, low HP. Good early-game transport for small squads. |
| Valkyrie         | $75,000| Engine + 1    | 280 | 13         | 2            | Primary troop transport. Good balance of capacity, durability, and armament. Workhorse of mid-game operations. |
| Hawk Air Warrior | $100,000| Engine + 0   | 460 | 19         | 3            | Heavy assault transport. Highest HP and largest crew capacity. Three weapon slots make it formidable in air combat. Expensive but durable. |
| Dimension Probe  | Special| Engine-based  | 80  | 0          | 0            | Unmanned research probe. Cannot carry passengers. Used to explore the alien dimension. Requires research to unlock. |

**Speed formula**: Vehicle speed is determined by the equipped engine plus a vehicle-specific
modifier. Lighter vehicles like the Hoverbike gain a larger bonus to their engine speed.

## Vehicle Weapons

Vehicles can be equipped with various weapon systems, purchased from organizations or
manufactured by X-COM.

| Weapon                  | Damage Type | Notes                                               |
|-------------------------|-------------|-----------------------------------------------------|
| Bolter 4K Laser Gun     | Laser       | Standard early-game vehicle laser. Low damage, high accuracy. |
| Lancer 7K Laser Gun     | Laser       | Upgraded laser. Better damage output.               |
| Rendor Plasma Gun       | Plasma      | Mid-game plasma weapon. Good damage and fire rate.  |
| Lineage Plasma Cannon   | Plasma      | Heavy plasma weapon. High damage, moderate fire rate.|
| Light Disruptor Beam    | Disruptor   | Light alien-tech weapon. Good damage, low weight.   |
| Medium Disruptor Beam   | Disruptor   | Medium alien-tech weapon. Excellent damage.         |
| Heavy Disruptor Beam    | Disruptor   | Heaviest vehicle weapon. Devastating damage output. |
| Janitor Missile Rack    | Explosive   | Missile launcher. High burst damage, limited ammo.  |
| Justice Missile Launcher| Explosive   | Heavy missile system. Devastating but slow to reload.|
| Stun Grapple            | Stun        | Non-lethal weapon for disabling UFOs without destroying them. |

## UFO Types

Alien UFOs appear through Dimensional Gates that open in the Mega-Primus airspace. Each UFO
type has a specific role in the alien invasion strategy.

| UFO Type        | Speed | HP   | Armor | Weekly Score | Role                                                   |
|-----------------|-------|------|-------|--------------|--------------------------------------------------------|
| Probe           | Low   | 40   | 5     | 5            | Reconnaissance. Scouts the city, rarely engages. Appears early in the invasion. |
| Scout Ship      | Med   | 80   | 8     | 10           | Light reconnaissance and early attack craft.           |
| Transporter     | Low   | 300  | 20    | 30           | Delivers aliens to buildings for infiltration and ground attacks. Primary infiltration vector. |
| Fast Attack Ship| High  | 150  | 12    | 20           | Hit-and-run attacker. High speed makes interception difficult. |
| Destroyer       | Med   | 400  | 25    | 50           | Heavy combat vessel. Dangerous in direct confrontation.|
| Assault Ship    | Med   | 500  | 30    | 75           | Heavy troop carrier for major assaults on buildings.   |
| Bomber          | Low   | 350  | 22    | 60           | Attacks city infrastructure. Can cause massive building damage and score penalties. |
| Escort          | Med   | 450  | 28    | 70           | Protects other UFOs. Often accompanies Transporters and Bombers. |
| Battleship      | Med   | 700  | 40    | 100          | Capital ship. Extremely dangerous. Heavy weapons and armor. |
| Mothership      | Low   | 1500 | 50    | 300          | Largest alien vessel. Appears in late game. Massive HP pool and devastating weapons. Shooting one down is a major victory. |

### UFO Behavior

- **Probes and Scouts**: Appear early. Fly around the city gathering intelligence. Generally
  avoid combat.
- **Transporters**: Land at or near buildings to deploy aliens for infiltration. High
  priority interception targets to prevent infiltration.
- **Bombers**: Target city buildings for destruction. Destroying buildings damages X-COM's
  score and relations with the building's owner.
- **Escorts**: Fly in formation with other UFOs to protect them. Engage X-COM vehicles that
  approach the escorted craft.
- **Battleships and Motherships**: Appear in the late game as the alien invasion escalates.
  Extremely difficult to bring down without advanced weapons.

## Ground vs Air Vehicles

X-COM primarily uses air vehicles (hover-capable craft) for rapid response across
Mega-Primus. Ground vehicles exist in the game as organization assets:

- **Ground vehicles** travel along the city's road network. They are slower but some are
  well-armored.
- **Air vehicles** fly directly between points and can engage UFOs in aerial combat.
- X-COM cannot purchase ground vehicles; all X-COM vehicles are air-capable.
- Organization ground vehicles may be encountered during raids or may be damaged as
  collateral during air combat.

## Vehicle Engines

Vehicle speed and range are determined by the equipped engine. Engines are upgraded through
research.

| Engine Type          | Source    | Notes                                              |
|----------------------|-----------|----------------------------------------------------|
| Standard Engines     | Purchase  | Basic engines available from Superdynamics and others. |
| Advanced Engines     | Research  | Improved thrust and efficiency. Researched from alien tech. |
| Elerium Engines      | Research  | Alien-derived engines using Elerium-115 fuel. Superior performance. Required for inter-dimensional travel. |

### Inter-Dimensional Travel

To access the Alien Dimension, vehicles must be equipped with Dimension Shift technology
(derived from Elerium engine research). Only vehicles with this capability can enter
dimensional gates and travel to the alien homeworld for the final campaign missions.

The Dimension Probe is the first vehicle capable of inter-dimensional travel and is used
to gather intelligence about the alien dimension before committing combat forces.

## Sources

- [Vehicles (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Vehicles_(Apocalypse))
- [UFOs (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=UFOs_(Apocalypse))
- [Vehicle Weapons (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Vehicle_Weapons_(Apocalypse))
- [Vehicle Equipment (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Vehicle_Equipment_(Apocalypse))
