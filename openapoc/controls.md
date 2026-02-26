# Controls

This document covers the complete control scheme for OpenApoc (version 0.0.49+). OpenApoc aims to implement all controls from the original X-COM: Apocalypse while introducing new hotkeys to improve usability. OpenApoc provides an **improved city control scheme** by default, with the option to fall back to vanilla controls.

---

## General UI Hotkeys

These hotkeys work across all screens and menus.

| Key | Action |
|---|---|
| Mousewheel | Scroll lists |
| Esc | Go back, close form, select "Cancel" option |
| Enter | Go forward, select "Confirm" option, select first option |
| Space | Skip, select second (non-cancel) option |

**Examples:**
- **Esc**: "OK" button in screens, "Cancel" or "No" option in dialogues
- **Enter**: "OK" option in screens, "Confirm" or "Yes" option in dialogues, real time in briefing
- **Space**: "No" in "Yes/No/Cancel" dialogue, equip button in squad assignment, checkbox to pause when event happens again, turn based in briefing

---

## General Map Hotkeys

These hotkeys work in both the Cityscape and Battlescape map views.

| Key | Action |
|---|---|
| Middle Click | Move camera to location |
| Arrow Keys | Move camera around |
| Tab | Toggle map |
| Space | Pause/Resume time (including turn-based) |
| Escape | Options menu |
| C | Toggle Follow Mode |
| M | Show Log |
| Home | Zoom to last event |

---

## Cityscape Controls

### Improved Control Scheme (Default)

OpenApoc introduces a new, consistent control scheme for the cityscape that addresses limitations in the original game. The original vanilla controls were inconsistent -- right-clicking moved the map in the city but not in battle, there were no quick-access hotkeys for frequently used screens, and Alt/Shift hotkeys acted like button clicks that could change selection mode if missed.

The improved scheme is enabled by default via the **"Improved city control scheme"** option (`OpenApoc.NewFeature.OpenApocCityControls`).

#### Mouse Controls

| Key | Action |
|---|---|
| Left Click | Issue orders; open Base screen for base buildings; open Building screen for other buildings |
| Right Click | Open Building screen for buildings |
| Ctrl + move order (Agents) | Force agents to move on foot (never call a taxi); allow use of personal teleporter |
| Ctrl + move order (Vehicles) | Allow manual use of teleporter |
| Ctrl + attack order | Force vehicles to attack target (instead of recovering UFOs or escorting owned vehicles) |
| Alt + Left Click | Open UFOpaedia screen for the object (vehicle type, building function, or projectile origin) |
| Alt + Right Click | Open UFOpaedia screen for the object's owner (vehicle or building) |
| Alt + Shift + Left Click | Order Attack Building |
| Alt + Shift + Right Click | Order Goto Building |
| Shift + Left Click | Order Attack Vehicle |
| Shift + Right Click | Order Follow Vehicle / Goto Location |

> **Note:** Attacking owned vehicles requires the `OpenApoc.NewFeature.AllowAttackingOwnedVehicles` option (enabled by default).

#### Keyboard Controls

| Key | Action |
|---|---|
| 0, 1, 2, 3, 4, 5 | Control time speed |
| N | Manual control |

### Vanilla Control Scheme

The vanilla control scheme can be re-enabled by disabling the **"Improved city control scheme"** option. When the vanilla scheme is active:

| Key / Action | Behavior |
|---|---|
| Right Click | Move screen to cursor |
| Alt + Left Click | Order vehicle attack |
| Shift + Left Click | Order moving to building |
| Left Click on building | Always open building screen |
| M | Manual control (N has no function) |

> **Note:** In vanilla mode, there is no way to open the message log (as per the original game), and none of the mouse controls introduced by OpenApoc will function.

---

## Vehicle / Agent Icon Clicks

When clicking on vehicle or agent icons in the cityscape UI:

| Key | Action |
|---|---|
| Shift + Right Click | Open Location Screen |
| Ctrl + Shift + Right Click | Open Equipment Screen |
| Alt + Shift + Right Click | Open Equipment Screen |

---

## Cityscape Unit Selection

| Key | Action |
|---|---|
| Left Click | Select Agent/Vehicle (as the only object selected) |
| Ctrl + Left Click | Add Agent/Vehicle to selection and make it first in the list |
| Right Click | Remove Agent/Vehicle from selection |

> **Note:** Ctrl makes selection additive.

---

## Vehicle Equipment

| Key | Action |
|---|---|
| Shift + click item | Auto-equip item into first available slot, or auto-remove to base stores |

---

## Agent Equipment

Standard selection controls apply, with the option to deselect with right click as well.

| Key | Action |
|---|---|
| Shift + click item | Auto-equip into first available slot, or auto-remove to base stores / ground |
| Ctrl + click weapon | Remove clip from weapon |
| 1 through 0 | Apply equipment template to every selected agent |
| Ctrl + 1 through 0 | Save current agent's equipment set as a template |

> **Note:** Equipment templates require the `OpenApoc.NewFeature.EnableAgentTemplates` option (enabled by default).

---

## Battlescape Controls

### Mouse Controls

| Key | Action |
|---|---|
| Left Click | Order unit to execute action at cursor (move / throw / psi attack / teleport etc.); open probed unit's screen; use item |
| Right Click | Turn towards cursor; focus at enemy in real-time; use item's "auto" function (e.g. prime grenade for impact) |
| Shift + Left Click | Order unit to fire at target tile, shot moving parallel to ground |
| Shift + Alt + Left Click | Order unit to fire at target tile, shot aimed at tile's ground |

**Modifier keys:**
- **Alt** when giving move orders: makes unit keep facing the target (unit strafes or moves backwards). When firing at a tile: makes the shot aim at the ground of the tile rather than at unit's level.
- **Shift** turns the cursor into attack mode.

### Battlescape Unit Selection

| Key | Action |
|---|---|
| Left Click | Select Unit (as the only unit selected) |
| Ctrl + Left Click | Add Unit to selection and make it first in the list |
| Right Click | Remove Unit from selection |

> **Note:** Ctrl makes selection additive.

### Keyboard Controls

#### Navigation

| Key | Action |
|---|---|
| PgUp / PgDown | Change map levels |
| V | Toggle layering |

#### Movement Modes

| Key | Action |
|---|---|
| F2 | Prone Mode |
| F3 | Walk Mode |
| F4 | Run Mode |
| Backspace | Kneel Mode |

#### Fire Modes

| Key | Action |
|---|---|
| F5 | Cease Fire Mode |
| F6 | Aimed Mode |
| F7 | Snap Mode |
| F8 | Auto Mode |

#### Behavior Modes

| Key | Action |
|---|---|
| F9 | Evasive Mode |
| F10 | Normal Mode |
| F11 | Aggressive Mode |

#### Squad and Unit Selection

| Key | Action |
|---|---|
| 1 through 6 | Select squad |
| Shift + 1 through 6 | Select Unit in current squad (as the only unit selected) |
| Shift + Ctrl + 1 through 6 | Add Unit to selection and make it first in the list |
| Alt + 1 through 6 | Cycle through spotted enemies of unit |

#### Actions

| Key | Action |
|---|---|
| Enter | Open Inventory |
| [ | Throw right hand item |
| ] | Throw left hand item |
| ' | Drop right hand item |
| \\ | Drop left hand item |
| Y | Confirm priming |
| N | Cancel priming |
| E | End your turn |
| S | Open Save menu |
| L | Open Load menu |
| J | Make unit jump (down from a cliff) |

---

## Notes

- OpenApoc eventually aims to implement all controls from the original game manual, plus new quality-of-life hotkeys (such as mouse scroll for lists).
- The `OpenApoc.NewFeature.BattlescapeVertScroll` option (default: true) allows the mousewheel to change vertical levels in the battlescape.
- The `OpenApoc.NewFeature.SingleSquadSelect` option (default: false) allows selecting a squad with a single click.
- The `OpenApoc.NewFeature.LeftClickIconEquip` option (default: false) makes left-clicking an icon open the equip menu.

Source: [`README_HOTKEYS.txt`](https://github.com/OpenApoc/OpenApoc/blob/master/README_HOTKEYS.txt)
