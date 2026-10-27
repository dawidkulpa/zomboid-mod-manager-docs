---
title: Overview
nav_order: 1
permalink: /
---

# Zomboid Mod Manager

A **Mods** page for every Project Zomboid server in Pterodactyl 2.0: add Steam Workshop mods, fix requirements and
load order, and apply with a backup first.
{: .fs-6 .fw-300 }

![The Installed tab]({{ '/assets/screenshots/01-installed.png' | relative_url }})

## Features

- [**Installed mods**](features/installed.md): every Workshop item and mod, with updates and problems.
- [**Adding mods**](features/browse.md): Workshop search, collections, or a link or ID (no API key needed).
- [**Missing requirements**](features/requirements.md): each one with a one-click fix.
- [**Load order and maps**](features/load-order.md), sorted by requirements.
- [**Apply, history and undo**](features/applying.md): stop, back up, save, start, as a job on the panel.
- [**Permissions**](features/permissions.md): View and Manage for subusers.

![Every step of an apply, shown while it runs]({{ '/assets/screenshots/06b-apply-progress.png' | relative_url }})

## Requirements

- Pterodactyl Panel 2.0 with its queue worker and scheduler, Wings 1.13+.
- Project Zomboid Build 42.
- Optional: a Steam Web API key.

[Installation](installation.md) · [Configuration](configuration.md) · [Support](support.md)
