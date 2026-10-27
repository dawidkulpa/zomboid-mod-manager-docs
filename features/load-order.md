---
title: "Load order"
parent: "Features"
nav_order: 4
---

# Load order

Project Zomboid loads mods in the order of the `Mods=` line, and a mod must load after the mods it requires. The
**Load order** tab shows the enabled mods in that order.

## Problems

- "Loads before X, which it needs": the order is wrong.
- "Needs X, which is not enabled": **Fix in Installed** opens the [fixes](requirements.md).

**Problems only** shows just these mods.

## Fixing the order

- **Sort by requirements** makes the smallest change that puts every mod after its requirements. It shows the mods
  that move; **Accept order** stages it.
- Drag a mod, or use its up and down buttons.
- Search filters the list without changing the order.

## Maps

The maps section lists the folders on the `Map=` line; reorder them with the up and down buttons. Custom maps load
before the base map, **Muldraugh, KY**, which stays last.

Changes are staged; [apply](applying.md) them.
