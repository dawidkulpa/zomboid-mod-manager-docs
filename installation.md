---
title: "Installation"
nav_order: 2
---

# Installation

## Requirements

- Pterodactyl Panel 2.0 (tested on 2.0.0-beta.2) with its **queue worker** and **scheduler** (`schedule:run` cron)
  running. Applies run as queued jobs; without a worker they never finish.
- Wings 1.13 or newer.
- Project Zomboid **Build 42**. Build 41 servers show a warning and are not supported.
- The server config at `.cache/Server/<SERVERNAME>.ini`, the default of the common eggs. Other paths:
  [Config file](configuration.md#config-file).
- Optional: a Steam Web API key, for Workshop search and collections. Adding mods by link or ID works without one.

Works on the stock panel and with themes installed through the panel's Themes page.

## Install

1. Get the package: copy the install command from the extension page or **Your purchases** on
   [pterodactyl.io](https://pterodactyl.io/marketplace) (its link works for 15 minutes), or download the
   `.pteroext` file from BuiltByBit.
2. In the panel directory:

   ```sh
   php artisan p:extension:install "<link or path to the .pteroext>" --enable
   php artisan queue:restart
   ```

3. Open **Admin › Extensions › Zomboid Mod Manager › Settings**. Check the config file path and, optionally, add a
   Steam Web API key. See [Configuration](configuration.md).
4. Open a Project Zomboid server. It has a **Mods** tab; if not, see
   [Which servers get the Mods page](#which-servers-get-the-mods-page).
5. For subusers, grant access in the server's **Users** tab. See [Permissions](features/permissions.md).

`php artisan p:extension:list` shows `zomboid-mods` as enabled.

## Which servers get the Mods page

A server gets the page when either is true:

- Its startup command runs `ProjectZomboid64` or `ProjectZomboid32`, as the eggs from pterodactyl/game-eggs,
  parkervcp and Pelican do, and [automatic detection](configuration.md#detect-project-zomboid-servers-automatically)
  is on (the default).
- Its egg has the tag `project-zomboid`. Use this for eggs that start the game another way, such as
  `start-server.sh`: create the tag in **Admin › Tags** and add it to the egg in **Admin › Eggs**.

Other servers have no Mods page. The extension never changes eggs or tags.

## Update

```sh
php artisan p:extension:install "<link or path to the .pteroext>" --enable --replace
php artisan queue:restart
```

Settings, history and the scan cache are kept.

## Disable or remove

| Command | Effect |
| --- | --- |
| `php artisan p:extension:disable zomboid-mods` | Hides the Mods page. Keeps files, settings and history. |
| `php artisan p:extension:remove zomboid-mods` | Removes the extension. Its tables (`zomboid_mods_*`) may stay; drop them if you want no data left. |

Neither changes a game server: mods, config and backups stay as they are.
