---
title: "Installed mods"
parent: "Features"
nav_order: 1
---

# Installed mods

The **Installed** tab lists the Workshop items on the server and the mods inside them. The header shows the item
count, enabled mods and disk size.

## Rows

- Preview, title, Workshop ID, number of mods, size and last update.
- **Enabled** switch. For an item with several mods, expand the row to switch each mod.
- **⋯** menu: **Open in Steam**, **Remove** (removes the item with all its mods).

| Label | Meaning |
| --- | --- |
| **Downloads on next start** | Added, not downloaded yet. |
| **Update available** | Steam has a newer version. The server downloads it on its next start; until then, players with the new version cannot join. |
| **N missing requirements** | Click it for the fixes. See [Missing requirements](requirements.md). |
| **Build 41 only** | The mod has no Build 42 folder. |
| **Map** | The item has a map folder; it goes on the `Map=` line automatically. |

## Search and filters

Search by title or mod ID. Filters: **All**, **Enabled**, **Disabled**, **Updates**, **Problems**.

## Changes are staged

Switching, adding and removing change nothing on the server yet. The bar at the bottom counts the changes:
**Discard** drops them, **Apply changes** opens the [apply dialog](applying.md).

The list is read from the server's files through Wings and cached per item. The first scan of a large server runs in
the background; the page stays usable.
