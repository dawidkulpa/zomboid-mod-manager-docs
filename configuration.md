---
title: "Configuration"
nav_order: 3
---

# Configuration

All settings are in **Admin › Extensions › Zomboid Mod Manager › Settings** and apply to every Project Zomboid
server on the panel. **Save Settings** checks every field first: if one is invalid, nothing is saved and the message
names the field.

| Setting | Default |
| --- | --- |
| [Detect Project Zomboid servers automatically](#detect-project-zomboid-servers-automatically) | On |
| [Config file](#config-file) | `.cache/Server/{SERVERNAME}.ini` |
| [Back up game data before applying changes](#back-up-game-data-before-applying-changes) | On |
| [Steam Web API key source](#steam-web-api-key-source) | One key for the panel |
| [Steam Web API key (panel-wide)](#steam-web-api-key) | None |
| [Steam calls per user per minute](#steam-call-limits) | 60 |
| [Steam calls per key per day](#steam-call-limits) | 80,000 |

## Detect Project Zomboid servers automatically

On: servers whose startup command runs `ProjectZomboid64` or `ProjectZomboid32` get the Mods page. Off: only eggs
with the tag `project-zomboid` do. The tag works either way. See
[Which servers get the Mods page](installation.md#which-servers-get-the-mods-page).

## Config file

The path of the server config, relative to the server root. An empty field saves the default.

- `{SERVERNAME}` is the server's `SERVERNAME` or `SERVER_NAME` startup variable, or `servertest` when it is empty.
  Any other `{VARIABLE}` is that startup variable.
- Refused on save: a path that leaves the server (`..`), a path without a file name, a variable not written as
  `{CAPITALS}`.
- If a variable is empty on one server, that server's Mods page says which one, and nothing can be applied there until
  it is set.

The extension changes three lines of the file and leaves every other byte as it is:

| Line | Content |
| --- | --- |
| `WorkshopItems=` | Workshop item IDs, separated by `;` |
| `Mods=` | Enabled mod IDs in load order, separated by `;` |
| `Map=` | Custom map folders, then the base map `Muldraugh, KY` |

On `Mods=`, existing entries keep their form and new ones follow the line's style. Build 42 loads `ModId` and
`\ModId` the same way. It does **not** load the hoster form `<WorkshopID>\ModId` (the log says
`required mod "…" not found`): replace such entries with the plain mod ID.

## Back up game data before applying changes

Whether **Back up the game data first** starts checked in the apply dialog. After that, each user's last choice is
remembered in their browser.

- The backup holds the game's data folder: with the default path, `.cache` (world, players, server settings). The game
  install and Workshop downloads are left out. If the config path is not inside a `Server` folder, the whole server is
  backed up.
- Backups count against the server's backup limit. At the limit, the oldest unlocked backup is deleted, as with
  scheduled backups. Lock the ones you want to keep.
- On servers with a backup limit of 0 the option is off.

## Steam Web API key source

| Option | Which key a server uses |
| --- | --- |
| **One key for the panel** | The panel key. |
| **Server keys, panel key as backup** | Its own key if it has one, otherwise the panel key. |
| **Server keys only** | Its own key. Without one, it works as without a key. |

In the server modes, the server owner or a subuser with **Manage** adds the key with **Steam key** on the Mods page.
The panel checks it with Steam before saving, stores it encrypted with `APP_KEY` and never shows it again. Saving and
removing a key are logged in the server's activity, without the key. If `APP_KEY` changes, stored server keys must be
entered again.

## Steam Web API key

1. Sign in to Steam with the account the panel should use and get a key at
   <https://steamcommunity.com/dev/apikey>. Steam requires an account that has spent at least USD 5 and asks for a
   domain: use the panel's.
2. Paste it into **Steam Web API key (panel-wide)** and save. The panel checks the format (32 characters, 0-9 and
   A-F) and makes one call to Steam; a refused key is not saved.

The key is stored encrypted and never shown again; the field reads "Stored: ********". Leave the field empty to keep
the key, or type a new one to replace it. The form cannot delete it: to stop using it, choose **Server keys only** or
revoke the key on Steam. Keys never reach the browser.

**Without a key** you still get the installed list (titles, previews, sizes, updates), adding mods by link or ID,
and the requirement fixes. **A key adds** Workshop search, collections, ratings, screenshots and Find on Workshop.

## Steam call limits

Steam allows about 100,000 calls a day per key. Only real calls to Steam count; cached answers are free. A Browse page
costs 1-3 calls. 0 turns a limit off.

| Setting | Default | Safe range | At the limit |
| --- | --- | --- | --- |
| **Steam calls per user per minute** | 60 | 30-120 | That user waits for the rest of the minute: "Too many Workshop requests, try again in N s." Others are not affected. |
| **Steam calls per key per day** | 80,000 | 50,000-90,000 | Search, collections, ratings and Find on Workshop pause until 00:00 UTC on every server using that key. Adding by link or ID keeps working. |

The daily limit is the one that protects the key: the per-user limit alone allows 86,400 calls a day per user. It is
counted per key: each server key has its own, and all servers on the panel key share one.
