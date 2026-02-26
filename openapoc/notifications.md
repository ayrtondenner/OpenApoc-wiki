# Pause Notifications

OpenApoc provides a comprehensive set of configurable pause notifications for both the Cityscape and Battlescape. When a notification triggers, the game pauses and displays an alert, giving the player time to react to important events.

All notifications are **enabled by default** and can be toggled individually in the game's notification settings. The configuration keys below correspond to entries in `settings.cfg` under the `Notifications.City` and `Notifications.Battle` sections.

---

## City Notifications

These notifications trigger during Cityscape gameplay. All default to **true** (enabled).

### Vehicle Status

| Config Key | Description | Default |
|---|---|---|
| `Notifications.City.VehicleLightDamage` | Vehicle lightly damaged | true |
| `Notifications.City.VehicleModerateDamage` | Vehicle moderately damaged | true |
| `Notifications.City.VehicleHeavyDamage` | Vehicle heavily damaged | true |
| `Notifications.City.VehicleDestroyed` | Vehicle destroyed | true |
| `Notifications.City.VehicleEscaping` | Vehicle damaged and returning to base | true |
| `Notifications.City.VehicleNoAmmo` | Weapon out of ammo | true |
| `Notifications.City.VehicleLowFuel` | Vehicle low on fuel | true |

### Vehicle Maintenance

| Config Key | Description | Default |
|---|---|---|
| `Notifications.City.VehicleRepaired` | Vehicle repaired | true |
| `Notifications.City.VehicleRearmed` | Vehicle rearmed | true |
| `Notifications.City.NotEnoughAmmo` | Not enough ammo to rearm vehicle | true |
| `Notifications.City.VehicleRefuelled` | Vehicle refuelled | true |
| `Notifications.City.NotEnoughFuel` | Not enough fuel to refuel vehicle | true |

### Agents and Personnel

| Config Key | Description | Default |
|---|---|---|
| `Notifications.City.AgentDiedCity` | Agent has died | true |
| `Notifications.City.AgentArrived` | Agent arrived at base | true |

### Cargo and Transfers

| Config Key | Description | Default |
|---|---|---|
| `Notifications.City.CargoArrived` | Cargo has arrived at base | true |
| `Notifications.City.TransferArrived` | Transfer arrived at base | true |
| `Notifications.City.RecoveryArrived` | Crash recovery arrived at base | true |

### Threats and Events

| Config Key | Description | Default |
|---|---|---|
| `Notifications.City.UfoSpotted` | UFO spotted | true |
| `Notifications.City.UnauthorizedVehicle` | Unauthorized vehicle detected | true |
| `Notifications.City.BaseDestroyed` | X-COM base destroyed by hostile forces | true |

---

## Battle Notifications

These notifications trigger during Battlescape gameplay. All default to **true** (enabled).

### Enemy Status

| Config Key | Description | Default |
|---|---|---|
| `Notifications.Battle.HostileSpotted` | Hostile unit spotted | true |
| `Notifications.Battle.HostileDied` | Hostile unit has died | true |
| `Notifications.Battle.UnknownDied` | Unknown unit has died | true |

### Unit Health and Casualties

| Config Key | Description | Default |
|---|---|---|
| `Notifications.Battle.AgentDiedBattle` | Unit has died | true |
| `Notifications.Battle.AgentBrainsucked` | Unit brainsucked | true |
| `Notifications.Battle.AgentCriticallyWounded` | Unit critically wounded | true |
| `Notifications.Battle.AgentBadlyInjured` | Unit badly injured | true |
| `Notifications.Battle.AgentInjured` | Unit injured | true |
| `Notifications.Battle.AgentUnderFire` | Unit under fire | true |

### Unit Status Effects

| Config Key | Description | Default |
|---|---|---|
| `Notifications.Battle.AgentUnconscious` | Unit has lost consciousness | true |
| `Notifications.Battle.AgentLeftCombat` | Unit has left combat zone | true |
| `Notifications.Battle.AgentFrozen` | Unit has frozen | true |

### Morale Events

| Config Key | Description | Default |
|---|---|---|
| `Notifications.Battle.AgentBerserk` | Unit has gone berserk | true |
| `Notifications.Battle.AgentPanicked` | Unit has panicked | true |
| `Notifications.Battle.AgentPanicOver` | Unit has stopped panicking | true |

### Psionic Events

| Config Key | Description | Default |
|---|---|---|
| `Notifications.Battle.AgentPsiAttacked` | Psionic attack on unit | true |
| `Notifications.Battle.AgentPsiControlled` | Unit under Psionic control | true |
| `Notifications.Battle.AgentPsiOver` | Unit freed from Psionic control | true |

---

## Summary

OpenApoc provides **19 City notifications** and **17 Battle notifications**, for a total of **36 configurable pause events**. This is a significant improvement over the original game, giving players fine-grained control over which events interrupt gameplay.

### City Notifications (19 total)

| Category | Count |
|---|---|
| Vehicle Status | 7 |
| Vehicle Maintenance | 5 |
| Agents and Personnel | 2 |
| Cargo and Transfers | 3 |
| Threats and Events | 3 |

### Battle Notifications (17 total)

| Category | Count |
|---|---|
| Enemy Status | 3 |
| Unit Health and Casualties | 6 |
| Unit Status Effects | 3 |
| Morale Events | 3 |
| Psionic Events | 3 |

---

## Configuration

Notifications can be configured in several ways:

1. **In-game settings menu** -- Toggle individual notifications through the notification settings screen.
2. **`settings.cfg` file** -- Edit the `[Notifications.City]` and `[Notifications.Battle]` sections directly.
3. **Checkbox on event popup** -- When a notification fires, a checkbox is typically available to disable that specific notification from firing again.

All notifications default to `true` (enabled). Setting a notification to `false` suppresses the corresponding pause event, though the game event itself still occurs normally.

---

Source: [`framework/options.cpp`](https://github.com/OpenApoc/OpenApoc/blob/master/framework/options.cpp)
