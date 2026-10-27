---
title: "Changelog"
nav_order: 6
---

# Changelog

## 0.4.1

- All settings are in the panel's standard place, **Admin › Extensions › Zomboid Mod Manager › Settings**, as one
  list in setup order. The separate admin page from 0.4.0 is gone; stored settings and keys are kept.
- The panel Steam key is checked with Steam before it is saved. Errors name the field.
- An empty config file field saves the default path.

## 0.4.0

- The enable switch reacts exactly where it is drawn (cursor and click area).
- A separate admin settings page (removed again in 0.4.1).

## 0.3.0

- **Steam Web API key source**: one panel key, server keys with the panel key as backup, or server keys only. Server
  keys are set on the Mods page, checked with Steam, stored encrypted and never shown again.
- Limits on Steam calls per user per minute (default 60) and per key per day (default 80,000).
- Steam "not found" answers are cached for an hour; collection imports list up to 1,000 items.
- Request URLs containing the key can never reach the panel log.

## 0.2.0

- Safer apply: stop → backup → save → start. A failed apply leaves the mods unchanged and starts a server it stopped.
  Applies resume after a queue worker restart.
- The apply is refused up front when the mod list changed on the server or the backup would be refused.
- Project Zomboid servers are detected from their startup command; the egg tag is optional.
- **Manage** includes **View**.
- Existing `Mods=` entries keep their form.
- Invalid config paths are refused on save; Build 41 servers show a warning.

## 0.1.3

- The backup holds only the game data folder (`.cache` by default), not the whole server.

## 0.1.2

- Likely compatibility patches are labelled "likely".

## 0.1.1

- Problems with fixes per case, bulk turn-off of likely patches, and Find on Workshop.

## 0.1.0

- First release: Installed, Browse Workshop, Load order and History; adding by search, link, ID or collection;
  multi-mod items; maps; updates; apply with backup and undo; View and Manage permissions.
