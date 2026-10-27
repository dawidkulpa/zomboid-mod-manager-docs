---
title: "Configuration"
nav_order: 3
---

# Configuration

All settings are in the panel's standard place for extension settings: **Admin › Extensions › Zomboid Mod Manager ›
Settings**. They apply to every Project Zomboid server on the panel. The form is one list, in the order an admin sets
them up:

1. [Detect Project Zomboid servers automatically](#detect-project-zomboid-servers-automatically)
2. [Config file](#config-file)
3. [Back up game data before applying changes](#back-up-before-changes-by-default)
4. [Steam Web API key source](#steam-web-api-key-source)
5. [Steam Web API key (panel-wide)](#steam-web-api-key)
6. [Steam calls per user per minute and Steam calls per key per day](#steam-call-limits)

**Save Settings** saves them all at once. The panel checks every value first; when one is wrong, nothing is saved and a
message names the field, for example "Config file: The config file setting must stay inside the server (no "..")." or
"Steam Web API key: Steam refused this key, so nothing was saved. …".

## Steam Web API key

Turns on Workshop search (the **Browse Workshop** tab), collection import, ratings, screenshots and the list of
required items in the details view. All Steam calls go from the panel to the official Steam Web API
(`api.steampowered.com`); no key ever reaches a browser.

- Get a key at <https://steamcommunity.com/dev/apikey> while signed in to the Steam account the panel should use.
  Steam only gives keys to accounts that have spent at least USD 5, and asks for a domain name: use the panel's
  domain.
- Paste it into **Steam Web API key (panel-wide)** and choose **Save Settings**. The panel checks that it has 32
  characters (0-9, A-F), then makes one call to Steam with it and saves it only if Steam accepts it; otherwise nothing
  is saved and the message says why. It is stored encrypted with the panel's `APP_KEY`.
- The form never shows the key again: while one is stored, the field reads "Stored: ******** - enter a new value to
  replace it". Leaving the field empty keeps the stored key; typing a new one replaces it after the same check.
- The panel key is not used in **Server keys only**; a stored key stays stored.
- The form has no way to delete a stored key (the panel keeps a secret when its field is left empty). To stop using
  it, choose **Server keys only**, or revoke it on the Steam page.

Without a key the extension still:

- shows the installed mods with their Workshop titles, previews, sizes and updates;
- adds mods by Workshop link or ID (**Add mods › Paste link or ID**);
- lists missing requirements and fixes them by turning mods on or likely compatibility patches off (**Find on Workshop** needs
  the key);
- shows "Unavailable without API key" where data needs the key, and an explanation on the Browse tab: for admins how
  to add a key, for other users whom to ask.

If Steam rejects the key, the Browse tab says so; check the key on the Steam page above.

## Steam Web API key source

Which key a server's Steam calls use: **Steam Web API key source**. The help under the field says what each choice means:

| Value | Meaning |
| --- | --- |
| **One key for the panel** (`global`, default) | Every server uses the panel key. |
| **Server keys, panel key as backup** (`server_fallback`) | A server's own key when it has one, otherwise the panel key. |
| **Server keys only** (`server`) | Every server needs its own key; the panel key is not used. Servers without one work as without a key. |

In the two server modes, the server owner and subusers with **Manage** add the server's key on its Mods page
(**Steam key** in the page header, or the card on the **Browse Workshop** tab while the server has none). The panel
checks the key once with Steam before saving it (a rejected key is not saved), stores it encrypted with the panel's
`APP_KEY` and never sends it back: the page only shows **Stored** and the date it was saved. Saving and removing a
key are recorded in the server's activity log, without the key. Users with View only see "Ask the server owner to
add a Steam Web API key". Switching back to **One key for the panel** keeps the stored server keys unused; a server's key
is deleted with the server.

If the panel's `APP_KEY` changes, stored server keys can no longer be read; those servers work as without a key
until someone saves their key again.

## Steam call limits

Steam allows about 100,000 calls a day per Web API key. Two limits keep one user, or many users together, from
using that up. Both count only real calls to Steam: answers the panel has cached (item details for hours, a Browse
page for 10 minutes) are free, so normal use stays far below them. A Browse page or a details view costs 1-3 calls.
Both counters live in the panel's cache (Redis on a typical panel), so they hold across all PHP workers. 0 turns a
limit off. The form accepts whole numbers from 0 to 10,000 (per user per minute) and 0 to 10,000,000 (per key per day).

| Setting | Default | Safe values | What happens at the limit |
| --- | --- | --- | --- |
| **Steam calls per user per minute** (`steam_user_rate`) | 60 | 30-120 | That user's next Steam call on that server is refused for the rest of the minute: "Too many Workshop requests, try again in N s." (HTTP 429 with `Retry-After`). Cached results and other users are not affected. |
| **Steam calls per key per day** (`steam_daily_budget`) | 80,000 | 50,000-90,000 | Workshop search, collections, ratings and Find on Workshop pause for every server using that key until 00:00 UTC; the Browse tab says until when. Adding mods by link or ID keeps working (keyless details). |

One user at N calls a minute can make at most N × 1,440 calls a day: 60 gives 86,400, so the per-user limit alone
does not protect the key. The daily budget does, no matter how many users there are; 80,000 leaves 20% headroom
below Steam's limit. The daily budget is counted per key (by a hash of the key, never the key itself): in the server
modes each server key has its own budget, and all servers on the panel-wide key share one.

Item lookups that Steam answers with "not found" are remembered for an hour, and a collection import lists at most
1,000 items, so neither can make a long series of calls.

## Config file

Where the server keeps its config, relative to the server's root directory. Default:
`.cache/Server/{SERVERNAME}.ini`. `{SERVERNAME}` is replaced with the value of the server's `SERVERNAME` (or
`SERVER_NAME`) startup variable, or the game's default name `servertest` when it is empty. Any other `{VARIABLE}` is
replaced with that startup variable.

Leaving the field empty saves the default path.

The panel refuses a value it can never use when you save it ("Config file: …"): a path that leaves the server (`..`), a path without a file name (such as `/`),
or a variable not written in capitals inside braces. A variable that is empty on one server shows on that server's
Mods page instead: admins see which variable is empty and where to fix it, other users are asked to contact an
admin. Nothing can be applied on that server until it is fixed.

The extension changes exactly three lines in this file and keeps every other byte as it was:

| Line | What the extension writes |
| --- | --- |
| `WorkshopItems=` | The Workshop item IDs the server downloads, `;`-separated. |
| `Mods=` | The enabled mod IDs in load order, `;`-separated. Each mod already on the line keeps the form it has there: `ModId`, `\ModId` or `<WorkshopID>\ModId`. A new mod gets a `\` when the line already uses one, and plain IDs on an empty line, as Build 42 itself writes them. Build 42 servers load `ModId` and `\ModId` alike. |
| `Map=` | Custom map folders, always ending with the base map `Muldraugh, KY`. |

Build 42 (checked on 42.21) removes every `\` when it reads the `Mods=` line, so `ModId` and `\ModId` load the same
mod. A hoster-style `<WorkshopID>\ModId` entry is read as `<WorkshopID>ModId` and that mod is not loaded (the server
log says `required mod "<WorkshopID>ModId" not found`). The extension keeps such entries as written; replace them
with the plain mod ID to load the mod.

## Back up before changes by default

**Back up game data before applying changes**: whether **Back up the game data first** starts checked in the apply dialog. Each user's last choice is remembered
per browser after that. On servers whose backup limit is 0 the option is always off and disabled.

The backup contains only the game's data folder: the folder that holds `Server/<SERVERNAME>.ini` in the
[config file](#config-file) path, `.cache` with the default path. That is the world (`Saves`), the player database
(`db`) and the server settings (`Server`), without the game install and the downloaded Workshop files. If the config
path is not inside a `Server` folder, the extension cannot tell which folder holds the data and backs up the whole
server; the checkbox then reads **Back up the server first**.

Backups count against the server's backup limit. When the limit is reached, the oldest unlocked backup is removed,
as with scheduled backups. Lock backups you want to keep in the server's **Backups** tab.

## Detect Project Zomboid servers automatically

On by default. Shows the Mods page on servers whose startup command runs `ProjectZomboid64` or `ProjectZomboid32`,
as the official Project Zomboid eggs do, without any egg tag. Turn it off to show the page only on eggs with the tag
`project-zomboid`. See [installation.md](installation.md#which-servers-get-the-mods-page).

## Related panel settings

- **Egg tag `project-zomboid`**: always shows the Mods page on the egg's servers, see
  [installation.md](installation.md#which-servers-get-the-mods-page).
- **Server backup limit** (Admin › Servers › server › Build configuration): 0 turns the backup option off for that
  server.
- **Subuser permissions**: see [features/permissions.md](features/permissions.md).
