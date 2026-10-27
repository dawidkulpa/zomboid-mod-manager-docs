---
title: "Load order"
parent: "Features"
nav_order: 4
---

# Load order

Project Zomboid loads mods from top to bottom of the `Mods=` line. A mod must load after the mods it requires.
The **Load order** tab shows the enabled mods in that order.

## Problems

A mod that loads before one of its requirements is marked, for example "Loads before SmarterStorage, which it
needs". A mod whose requirement is not enabled at all is marked "Needs X, which is not enabled" with **Fix in
Installed**, which opens its item on the Installed tab with the fixes ([requirements.md](requirements.md)).
**Problems only** shows just those mods.

## Fixing the order

- **Sort by requirements** computes the smallest change that puts every mod after its requirements; other mods
  keep their relative order. A preview lists the mods that move; **Accept order** stages it.
- Move a mod by dragging it, or with its up and down buttons (keyboard friendly).
- Search filters the list without changing the order.

## Maps

Custom maps load before the base map. The maps section lists the map folders from the `Map=` line; reorder them
with the up and down buttons. **Muldraugh, KY** (the base map) is always last and locked.

Changes are staged; apply them as described in [applying.md](applying.md).
