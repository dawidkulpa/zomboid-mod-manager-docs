---
title: "Installation"
nav_order: 2
---

# Installation

Zomboid Mod Manager adds a **Mods** page to Project Zomboid servers on a Pterodactyl 2.0 panel. This guide covers
installing, updating and removing it. Settings are described in [configuration.md](configuration.md); the page
itself in [the feature guides](features/).

## Requirements

- Pterodactyl panel 2.0 (tested on 2.0.0-beta.2) with its queue worker and scheduler running. Applying changes and
  the first scan of a large server run as queued jobs; without a worker they never finish. The scheduler (the
  panel's `schedule:run` cron entry) picks up an apply whose job was lost in a worker restart.
- Project Zomboid **Build 42** servers. Build 41 servers are not supported: the Mods page shows a warning on them and
  mods may be shown incorrectly.
- Wings 1.13 or newer on the node that hosts the server.
- A Project Zomboid egg that keeps the server config in `.cache/Server/<SERVERNAME>.ini` (the default of the common
  Project Zomboid eggs). Another location can be set, see [configuration.md](configuration.md#config-file).
- Optional: a Steam Web API key for Workshop search and collections. Adding mods by link or ID works without one.

The extension uses only the panel's own extension system and theme tokens. It works on the stock panel and with
themes installed through the panel's Themes page.

## Install

1. Get the install command or the package:
   - bought through the [Pterodactyl marketplace](https://pterodactyl.io/marketplace): copy the install command from
     the extension page or from **Your purchases**. Its link works for 15 minutes.
   - bought on BuiltByBit: download `zomboid-mods-<version>.pteroext` and copy it to the panel host.
2. Install and enable it from the panel directory, then restart the queue worker:

   ```sh
   php artisan p:extension:install "<link from the install command>" --enable
   # or, with the downloaded package:
   php artisan p:extension:install zomboid-mods-<version>.pteroext --enable

   php artisan queue:restart
   ```

   Enabling runs the extension's database migrations (tables prefixed `zomboid_mods_`) and publishes its
   frontend. `queue:restart` makes the queue worker load the new code.
3. Check that your Project Zomboid servers show a **Mods** tab. Servers of the common Project Zomboid eggs are
   detected automatically; for other eggs add the tag `project-zomboid`, see
   [Which servers get the Mods page](#which-servers-get-the-mods-page).
4. Open **Admin › Extensions**, find **Zomboid Mod Manager** and choose **Settings**: every setting of the extension
   is there, in one list. Check the config file path (the default fits the common eggs) and, optionally, paste a
   Steam Web API key into **Steam Web API key (panel-wide)**. See [configuration.md](configuration.md).
5. Give subusers access in each server's **Users** tab: the group "Project Zomboid mods" has **View** and
   **Manage**. See [features/permissions.md](features/permissions.md).

Check the installation with `php artisan p:extension:list`: `zomboid-mods` should be listed as enabled.

## Which servers get the Mods page

The **Mods** page appears on a server when either is true:

- its startup command runs the Project Zomboid server (`ProjectZomboid64` or `ProjectZomboid32`), as the eggs from
  pterodactyl/game-eggs, parkervcp and Pelican do. The setting **Detect Project Zomboid servers automatically**
  (on by default, see [configuration.md](configuration.md#detect-project-zomboid-servers-automatically)) controls
  this;
- its egg has the tag `project-zomboid`. Use this for eggs that start the game another way, for example through
  `start-server.sh`: in **Admin › Tags** create a tag with the slug `project-zomboid` and give it to the egg in
  **Admin › Eggs**. The tag works whatever the setting says.

Other servers do not show the page, and its API answers 404 for them. The extension never changes eggs or tags.

## Update

Install the newer package over the old one and restart the queue worker:

```sh
php artisan p:extension:install zomboid-mods-<new-version>.pteroext --enable --replace
php artisan queue:restart
```

Settings, the scan cache and the change history are kept.

## Disable or remove

- `php artisan p:extension:disable zomboid-mods` hides the page and keeps files, settings and history.
- `php artisan p:extension:remove zomboid-mods` removes the extension's files, published assets and install record.
  The panel does not document that it drops the extension's tables (`zomboid_mods_items`, `zomboid_mods_applies`,
  `zomboid_mods_history`); drop them yourself if you want no data left.

Neither command changes any game server: installed mods, the server config and the backups the extension made stay
as they are.
