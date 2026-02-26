# City Management (X-COM: Apocalypse)

This document covers the strategic city management layer of the original X-COM: Apocalypse
(1997). Unlike previous X-COM games, Apocalypse takes place entirely within a single
futuristic megacity, where relationships with dozens of organizations form the core strategic
challenge alongside the alien threat.

## Mega-Primus

Mega-Primus is a massive, self-contained megacity of the year 2084. It is the last major
human city after global environmental collapse, built to house millions under a series of
interconnected domes and arcologies. The city is divided into districts controlled by various
organizations, each owning buildings, vehicles, and territory.

The cityscape is rendered in real-time, with vehicles flying through the air, UFOs appearing
through dimensional gates, and X-COM interceptors scrambling to respond. Buildings can be
damaged or destroyed during combat, which has diplomatic consequences.

## Organizations

Mega-Primus contains approximately 27 organizations, each with their own agenda, resources,
and relationships. X-COM must maintain positive relations with most organizations to secure
funding, equipment purchases, and intelligence cooperation.

### Government

| Organization          | Role                                                                  |
|-----------------------|-----------------------------------------------------------------------|
| Megapol               | City police force. Provides basic weapons, armor, and vehicles. Key early-game supplier. Responds to alien incursions. |
| Senate                | Governing body of Mega-Primus. Primary X-COM funding source. Relationship with the Senate directly affects weekly funding. |

### Military / Security

| Organization          | Role                                                                  |
|-----------------------|-----------------------------------------------------------------------|
| Marsec                | Private military corporation. Supplies advanced weapons and armor. Key mid-game equipment source. |
| X-COM                 | The player's organization. Operates independently but depends on other organizations for funding and supplies. |

### Transport

| Organization          | Role                                                                  |
|-----------------------|-----------------------------------------------------------------------|
| Transtellar           | Major transportation conglomerate. Operates People Tubes (public transit network). Controls critical infrastructure. |
| General Metro         | Road vehicle operator. Provides ground transport services.            |
| Superdynamics         | Aerospace manufacturer. Supplies vehicles and vehicle components.     |

### Science / Technology

| Organization          | Role                                                                  |
|-----------------------|-----------------------------------------------------------------------|
| Nanotech              | Nanotechnology research firm. Supplies advanced medical and scientific equipment. |
| Cyberweb              | Cybernetics and computing corporation. Supplies electronic components and cyber-equipment. |

### Energy

| Organization          | Role                                                                  |
|-----------------------|-----------------------------------------------------------------------|
| Solmine               | Solar energy mining corporation. Controls energy production facilities. |
| Energen               | Energy distribution corporation. Operates power infrastructure.       |

### Consumer / Media

| Organization          | Role                                                                  |
|-----------------------|-----------------------------------------------------------------------|
| Nutrivend             | Food production and distribution. Controls food supply.               |
| Evonet                | Entertainment and media network.                                      |
| Sensovision           | Virtual reality entertainment provider.                               |
| Lifetree              | Bioengineering and agriculture corporation.                           |
| Synthemesh            | Synthetic materials manufacturer.                                     |

### Political

| Organization          | Role                                                                  |
|-----------------------|-----------------------------------------------------------------------|
| Technocrats           | Pro-technology political faction. Generally supportive of X-COM.      |
| Extropians            | Transhumanist political faction. Neutral to positive toward X-COM.    |
| SELF (Sentient Engine Liberation Front) | Android rights activists. Can become hostile if Androids are mistreated. |
| Mutant Alliance       | Mutant rights organization. Can provide Hybrid agents.                |
| Sanctuary Clinic      | Medical and humanitarian organization. Provides medical services.     |

### Criminal

| Organization          | Role                                                                  |
|-----------------------|-----------------------------------------------------------------------|
| Osiron                | Organized crime syndicate. Operates black market. Can be raided for funds and equipment. |
| Diablo                | Street gang. Hostile and territorial. Minor threat.                   |
| Psyke                 | Drug-dealing gang. Minor threat.                                      |
| Grav Ball League      | Sports organization with criminal connections.                        |

### Pro-Alien

| Organization          | Role                                                                  |
|-----------------------|-----------------------------------------------------------------------|
| Cult of Sirius        | Alien-worshipping cult. Actively aids alien infiltration. Often hostile to X-COM. Grows stronger as alien influence increases. |

## Diplomacy System

Each organization has a relationship score with X-COM and with every other organization.
These scores range from hostile to allied and affect interactions.

### What Affects Relationships

| Action                          | Effect on Relationship                                             |
|---------------------------------|--------------------------------------------------------------------|
| Collateral damage to buildings  | Negative. Damaging or destroying an organization's property during combat (UFO interception, tactical missions) reduces their opinion of X-COM. |
| Raiding organization buildings  | Strongly negative. Sending agents to raid an organization's buildings is an act of aggression. |
| Alien infiltration              | Negative (indirect). As aliens infiltrate an organization, that organization becomes increasingly hostile to X-COM and friendly to aliens. |
| Bribes                          | Positive. X-COM can spend money to improve relations with any organization. |
| Defending city from aliens      | Positive. Successfully shooting down UFOs and resolving alien incidents improves relations with most organizations. |
| Recovering alien artifacts      | Positive (indirect). Advancing research and technology impresses organizations. |
| Organization rivalries          | Indirect. Some organizations are natural rivals; improving relations with one may strain relations with its rival. |

### Consequences of Relationship Levels

- **Allied**: The organization actively cooperates. Best equipment prices, intelligence sharing.
- **Friendly**: Good cooperation. Favorable prices.
- **Neutral**: Standard interactions. Default starting state for most organizations.
- **Unfriendly**: Reduced cooperation. Higher prices, may refuse sales.
- **Hostile**: The organization actively opposes X-COM. May attack X-COM vehicles and agents. Cuts off all trade.

## Alien Infiltration

Alien infiltration is one of the central strategic threats in X-COM: Apocalypse. Aliens
do not simply attack the city militarily; they also subvert it from within.

### Micronoid Infiltration

Micronoids are microscopic alien organisms that can take control of human hosts. They spread
through the city primarily via the **People Tube** network (Mega-Primus's public transit
system operated by Transtellar).

- Aliens introduce Micronoids into the People Tube system.
- Micronoids spread to organization staff who use the People Tubes.
- As more personnel of an organization become infected, the organization's infiltration
  percentage rises.
- Infiltration is invisible to the player unless detected through intelligence or obvious
  behavioral changes.

### Infiltration Consequences

| Infiltration Level | Effect                                                                  |
|--------------------|-------------------------------------------------------------------------|
| Low (1-25%)        | Minor behavioral changes. Organization may become slightly less cooperative. |
| Medium (26-50%)    | Noticeable hostility increase. Organization begins to resist X-COM activities. |
| High (51-75%)      | Organization actively aids aliens. May attack X-COM or refuse all cooperation. |
| Critical (76-99%)  | Organization is effectively an alien puppet. Highly hostile to X-COM.   |
| Complete (100%)    | **Permanent hostile alliance with aliens.** The organization is irreversibly lost. Cannot be recovered through any means. |

Reaching 100% infiltration on a critical organization (such as Megapol or the Senate) can
be catastrophic for the player's campaign.

### Countering Infiltration

- **Raid buildings**: X-COM can assault infiltrated organization buildings to root out aliens,
  but this damages the relationship with that organization.
- **Defend People Tubes**: Intercepting alien activity near People Tube infrastructure can
  slow infiltration spread.
- **Eliminate alien sources**: Destroying alien dimension gates and UFOs reduces the rate of
  new Micronoid introduction.

## Organization Rivalries and Alliances

Organizations in Mega-Primus have pre-existing relationships with each other that affect
the strategic landscape:

- **Megapol vs Criminal Organizations**: Megapol is naturally hostile toward Osiron, Diablo,
  and Psyke. Improving relations with criminals hurts Megapol relations.
- **SELF vs Organizations Using Androids**: SELF opposes organizations that use Androids as
  disposable labor.
- **Cult of Sirius vs X-COM**: The Cult is inherently opposed to X-COM's mission and
  grows more powerful as alien influence increases.
- **Senate and Megapol**: Generally aligned. If the Senate turns hostile, Megapol often
  follows.
- **Corporate rivalries**: Various corporations compete with each other, creating a web of
  shifting alliances.

These inter-organization dynamics mean that the player cannot simply maximize relations with
everyone. Strategic choices about which organizations to prioritize are necessary.

## Community Research

The following information has been gathered from OpenApoc Discord community research,
including reverse engineering of the original executable and extensive playtesting.

### Organization Relations Internal Mechanics

According to reverse engineering by community contributor skin36, the organization relations
system is more complex internally than the single displayed value suggests:

- Each organization pair has **4 relationship values**: short-term and long-term, in both
  directions (A->B and B->A).
- Relationship changes are processed through a `calc_relation()` function that applies either
  **-5 or -15** to the relevant values depending on the severity of the action.
- **Short-term values are updated at midnight** each game day, decaying toward a baseline.
- Save game files contain **three copies** of the relationship data (likely for redundancy or
  as a vestige of debugging).

### "Enemy of My Enemy" Mechanic

According to community testing on Novice difficulty, the commonly cited "enemy of my enemy is
my friend" mechanic **may not work as described** in the UFOpaedia. Attacking Organization A
did not make Organization B friendlier, despite the organizations being rivals. This needs
further testing at other difficulty levels to confirm whether it is universally broken or
difficulty-dependent.

### Alliance System (Cut Feature)

Community research has uncovered a cut alliance system in the original game code:

- An organization would offer a formal alliance if **both** of the following conditions were
  met:
  - Relationship with X-COM was **friendly (>25)**.
  - The organization shared **2 or more common enemies** with X-COM.
- A **commander-rank boss** from the organization would physically come to an X-COM base to
  offer the alliance.
- This system was cut before release but code remnants remain in the executable.

### Transport Vehicle Generation Formula

From the original disassembly (skin36), civilian transport vehicle generation follows an
**hourly distribution** that controls the maximum number of new vehicles spawned per hour:

```
Hour:  0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23
Max:   4  2  2  2  2  2  4  8 12  8  6  4 10  8  6  4  4 12 12  8  4  4  4  4
```

This creates a realistic traffic pattern with peaks during commuting hours (08:00, 12:00,
17:00-18:00) and low traffic during nighttime hours.

### Market Economy Details

According to community testing:

- **Buy and sell prices are not separate** -- there is a single price for each item that
  applies to both buying and selling.
- **Flooding the market** with manufactured goods **crashes the price** for that item. Selling
  large quantities of the same item rapidly devalues it.
- The **Psiclone** (psi-detection device) was a popular early-game money-maker, netting
  approximately **$4,500 per unit** until market saturation drives the price down.

### Government Funding Details

Community research has confirmed:

- If the government (Senate) becomes **hostile to X-COM**, funding drops to **zero**.
- Government funding also **decreases proportionally** with a negative weekly score,
  independent of the relationship level.

### Gravball League and Recruitment

According to community testing, the **Gravball League** affects agent recruitment indirectly
through its influence on civilian organization happiness. Positive Gravball League relations
can improve the pool of available recruits.

## Sources

- [Organizations (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Organizations_(Apocalypse))
- [Alien Infiltration (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Alien_Infiltration_(Apocalypse))
- [Mega-Primus - UFOpaedia](https://www.ufopaedia.org/index.php?title=Mega-Primus)
- [Diplomacy (Apocalypse) - UFOpaedia](https://www.ufopaedia.org/index.php?title=Diplomacy_(Apocalypse))
