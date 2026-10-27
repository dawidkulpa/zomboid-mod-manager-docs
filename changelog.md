---
title: "Changelog"
nav_order: 6
---

# Changelog

## 0.4.1

- All settings in one list, in setup order, in **Admin › Extensions › Zomboid Mod Manager › Settings**, with
  clearer labels and help.
- The panel Steam key is checked with Steam before it is saved. Errors name the field.
- An empty config file field saves the default path.

## 0.4.0

- The enable switch has a hover ring, and its click area matches the switch.

## 0.3.0

- **Steam Web API key source**: one panel key, server keys with the panel key as backup, or server keys only. Server
  keys are set on the Mods page, checked with Steam, stored encrypted and never shown again.
- Limits on Steam calls per user per minute (default 60) and per key per day (default 80,000).
- Steam "not found" answers are cached for an hour; collection imports list up to 1,000 items.
- Steam keys are kept out of the panel log.

## 0.2.0

- Safer apply: stop → backup → save → start. A failed apply leaves the mods unchanged and starts a server it stopped.
  Applies resume after a queue worker restart.
- The apply is refused up front when the mod list changed on the server or the backup would be refused.
- Project Zomboid servers are detected from their startup command; the egg tag is optional.
- **Manage** includes **View**.
- `Mods=` entries keep the form they are written in.
- Invalid config paths are refused on save; Build 41 servers show a warning.

## 0.1.3

- Smaller backups: only the game data folder (`.cache` by default).

## 0.1.2

- Likely compatibility patches are labelled "likely".

## 0.1.1

- Problems with fixes per case, bulk turn-off of likely patches, and Find on Workshop.

## 0.1.0

- First release: Installed, Browse Workshop, Load order and History; adding by search, link, ID or collection;
  multi-mod items; maps; updates; apply with backup and undo; View and Manage permissions.
