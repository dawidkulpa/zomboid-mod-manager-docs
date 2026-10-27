---
title: "Installed mods"
parent: "Features"
nav_order: 1
---

# Installed mods

The **Installed** tab lists the Workshop items the server downloads (`WorkshopItems=`) and the mods inside them.
The header shows totals: Workshop items, enabled mods and disk size.

## What a row shows

- Preview, Workshop title and ID, number of mods inside, size and last update.
- **Enabled** switch. For an item with several mods, expand the row to switch each mod on or off.
- Labels when something needs attention:
  - **Downloads on next start**: added but not downloaded yet. The server downloads it when it starts.
  - **Update available**: Steam has a newer version than the server. The server downloads it on its next start;
    until then players with the new version cannot join (**Restart to update** explains this).
  - **N missing requirements**: enabled mods of this item require mods that are not enabled. Click the label to see
    each one with its fix (turn a mod on, turn a likely patch off, or find the mod on the Workshop); see
    [requirements.md](requirements.md).
  - **Build 41 only**: the mod has no Build 42 folder.
  - **Map**: the item brings a map folder; it is placed on the `Map=` line automatically.
- The **⋯** menu: **Open in Steam** and **Remove** (asks for confirmation; removes the item and all its mods).

## Search and filters

Search by Workshop title or mod ID. The filter switches between **All**, **Enabled**, **Disabled**, **Updates** and
**Problems**. **Problems** opens every listed item's requirement list and offers to turn off all likely patches
at once.

## How the list is read

The extension reads the server's files through Wings: the Workshop download folder, the Workshop manifest and each
mod's `mod.info`. Results are cached per Workshop item, so only new or changed items are read again. The first scan
of a large server runs in the background with a progress bar; the page stays usable.

Workshop titles, previews and update times come from the Steam Web API and are cached for several hours. They work
without an API key.

## Changes are staged

Switching mods, adding or removing items does not touch the server yet. A bar at the bottom counts the changes;
**Discard** drops them and **Apply changes** opens the apply dialog, see [applying.md](applying.md).
