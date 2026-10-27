---
title: Overview
nav_order: 1
permalink: /
---

# Zomboid Mod Manager

Steam Workshop mods for Project Zomboid servers, managed from the server's own page in Pterodactyl 2.0.
{: .fs-6 .fw-300 }

Adding a mod to a Project Zomboid server usually means copying a Workshop ID, finding the mod IDs inside the item
and editing two lines of an ini file without breaking the load order. Zomboid Mod Manager adds a **Mods** page to
every Project Zomboid server on your panel, so you and your users can do it in a few clicks, and undo it when
something goes wrong.

![The Installed tab: every Workshop item on the server, with filters for enabled mods, updates and problems]({{ '/assets/screenshots/01-installed.png' | relative_url }})

## What it does

- **Browse the Steam Workshop** from the panel: search, sort, filter by category or *Works on Build 42*, open any
  item for screenshots, size, description and requirements. [Adding mods](features/browse.md)
- **Add mods any way you like**: a Workshop link or ID (no API key needed), a whole collection, or a search result.
  Pick the mods inside multi-mod items; map folders go on the `Map=` line automatically.
- **Fix missing requirements** with the fix that fits each case. [Missing requirements](features/requirements.md)
- **Load order and maps**, with *Sort by requirements*. [Load order](features/load-order.md)
- **Apply safely**: stop, back up the game data, save the mod list, start again, as a queued job on the panel.
  [Applying, history and undo](features/applying.md)
- **History and undo** for every applied change.
- **Permissions** for subusers: View and Manage. [Permissions](features/permissions.md)

![Every step of an apply is shown while it runs]({{ '/assets/screenshots/06b-apply-progress.png' | relative_url }})

## Requirements

- Pterodactyl Panel **2.0** (beta; tested on 2.0.0-beta.2) with its queue worker and scheduler running.
- Wings **1.13** or newer.
- Project Zomboid **Build 42** servers. Build 41 is not supported.
- Optional: a Steam Web API key for Workshop search, collections, ratings and screenshots.

Start with [Installation](installation.md), then [Configuration](configuration.md).

## Help

Questions, bugs and ideas: see [Support](support.md).
