---
title: "Changelog"
nav_order: 6
---

# Changelog

## 0.4.1

Settings back in the standard place

- All settings are in the panel's standard extension settings again: **Admin › Extensions › Zomboid Mod Manager ›
  Settings**, so they are found where every extension keeps them. The separate admin page **Admin › Zomboid Mods**
  from 0.4.0 is removed, with its navigation entry; installing 0.4.1 over 0.4.0 drops the entry. Stored settings and
  the panel Steam key are kept as they are.
- The form is one list without a section picker, in setup order: Detect Project Zomboid servers automatically,
  Config file, Back up game data before applying changes, Steam Web API key source, Steam Web API key (panel-wide),
  Steam calls per user per minute, Steam calls per key per day. Labels and help are shorter and say the consequence
  first; the key source options keep the 0.4.0 names.
- The panel-wide Steam key is a field of the form again. Leaving it empty keeps the saved key; a new key must have 32
  characters (0-9, A-F) and is checked with one call to Steam before anything is saved. A refused save names the
  field ("Steam Web API key: Steam refused this key, so nothing was saved. …"), as do config path and limit errors.
- An emptied config file field saves the default path instead of an empty value.
- Dropped with the page, because the standard form cannot show them: the detected servers list, **Check file**,
  **Test key**, **Remove** for the panel key, and today's Steam call count. To stop using the panel key, choose
  **Server keys only**.
- Messages on the Mods page that sent admins to Admin › Zomboid Mods now point to Admin › Extensions › Zomboid Mod
  Manager › Settings.

## 0.4.0

Settings page

- New admin page **Admin › Zomboid Mods** with every setting on one page, in the order an admin sets them up:
  **Servers**, **Backups**, **Steam Workshop**. No section picker; unsaved changes show a bar with **Discard** and
  **Save changes**, leaving the page asks first, and the panel answers invalid values with a message under the field.
- **Servers** lists the servers that have the Mods page and why (egg tag or startup command), shows which ones lose or
  gain the page before you save the detection switch, previews the config file path on a chosen server and can check
  that the file exists on its node.
- **Steam Workshop**: the key source is a choice of three cards, each with its consequence. The panel key shows its
  state ("Key saved · added 27 Oct 2026" or "No key") with **Test key**, **Replace** and **Remove**, instead of a
  masked value; a new key is checked for its format and with Steam before it is saved, and is never sent back. The
  panel key is hidden in "Server keys only", where it is not used. The limits show their defaults, safe ranges and
  today's calls of the panel key.
- The panel's generic settings form (Admin › Extensions › Settings) edits the same settings without sections and no
  longer holds the Steam key; existing settings and the stored key are kept as they are.
- Messages that sent admins to Admin › Extensions now point to Admin › Zomboid Mods.

Mods page

- The enable switch is the hover and click target exactly where it is drawn: the hand cursor and a hover ring show
  on the switch itself, not a few pixels above or below it.

## 0.3.0

Steam Web API key

- New setting **Steam Web API key source**: one panel-wide key for every server (default, as before), a server's own
  key with the panel-wide key as fallback, or only servers' own keys.
- In the server modes, the server owner and subusers with **Manage** add the server's key on its Mods page (**Steam
  key** in the header, or a card on the Browse tab while there is none), with how to get one. The key is checked with
  Steam before it is saved, stored encrypted with the panel's `APP_KEY`, never sent back to the browser, and saving or
  removing it is logged in the server's activity without the key. View-only users are told to ask the server owner.
- HTTP client errors are reduced to a fixed message before they can reach the panel's log, so a request URL with
  `key=` can never be logged.

Steam call limits

- New settings **Steam calls per user per minute** (default 60) and **Steam calls per key per day** (default 80,000,
  20% below Steam's 100,000 a day), with safe ranges in their help text; 0 turns a limit off. Only real calls to Steam
  count, cached answers are free.
- Over the per-user limit, Steam calls answer HTTP 429 with `Retry-After` and the Browse tab says "Too many Workshop
  requests, try again in N s." When a key's daily calls are used up, Workshop search pauses until 00:00 UTC and the
  page says until when; adding by link or ID keeps working.
- "Not found" answers from Steam are remembered for an hour, and a collection import lists at most 1,000 items.
- The extension settings are grouped on two tabs, **Steam Workshop** and **General** (replaced by the settings
  page in 0.4.0).

## 0.2.0

Applying changes

- The server is stopped first, then backed up, then the mod list is written, then (if chosen) it is started. The
  backup now holds the world exactly as the game saved it on shutdown. The progress steps and docs follow the new
  order.
- When an apply fails before the mod list is saved and the apply had stopped the server, the server is started
  again, and the message says so ("Your mods were not changed. The server was stopped for this change and has been
  started again").
- A config changed on the server since the page was loaded, or a backup the panel would refuse (its rate limit, all
  backups locked at the limit), is refused when you click **Apply changes**, before the server is stopped.
- Short node outages (a Wings restart, a network blip) are retried for two minutes instead of failing the apply.
- Nothing is written to a server that was started during the backup, and the power state is checked right before
  writing; an unknown power state counts as running.
- A user who applied while the server was offline and may not stop it no longer stops a server someone started
  meanwhile; the apply ends with "The server was started meanwhile".
- An apply no longer stalls with the server stopped: a run that finds another run busy comes back, a killed queue
  run is picked up again (up to three times, then the apply fails and restarts the server if needed), the config is
  never written near the end of a worker's time, and the panel's scheduler wakes lost applies every minute without
  anyone opening the Mods page.

Mods line

- Each mod already on the `Mods=` line keeps its form (`ModId`, `\ModId` or `<WorkshopID>\ModId`); before, the
  Workshop ID of the hoster form was dropped on every apply. A fresh Build 42 config gets plain IDs, as the game
  writes them.

Visibility and permissions

- Project Zomboid servers are detected from their startup command (`ProjectZomboid64`), so the official eggs get the
  Mods page without the `project-zomboid` egg tag. New setting **Detect Project Zomboid servers automatically** (on
  by default); the tag keeps working.
- A subuser with only **Manage** now sees the Mods tab and the progress of applies and scans (**Manage** includes
  **View** everywhere).

Errors and warnings

- A config path setting that cannot work (a path outside the server, an empty path, a malformed `{VARIABLE}`) is
  refused when saved. A startup variable that is empty on one server shows a clear message on its Mods page (what to
  fix for admins, whom to ask for others) instead of an error page.
- Build 41 servers show a warning on the Mods page. Zomboid Mod Manager supports Build 42 only.

## 0.1.3

- The backup before a change contains only the game data folder (the folder that holds `Server/<SERVERNAME>.ini`,
  `.cache` by default), not the game install and Workshop downloads. The whole server is backed up when the folder
  cannot be told.

## 0.1.2

- An optional patch whose requirement is missing is described with its uncertainty ("likely a compatibility patch").

## 0.1.1

- Problems: every unmet requirement with fixes by case, bulk turn-off of optional patches and a link to the load
  order.
- Find on Workshop: the Workshop items that hold a missing mod id, from the Steam Web API.
- Turned-on requirements load before the mod that needs them; an empty Problems state; "Not enough ratings" below
  the vote threshold.

## 0.1.0

- First release: the Mods page with Installed, Browse Workshop, Load order and History; adding mods by search, link,
  ID or collection; picking the mods inside multi-mod items; maps; updates; applying with an optional backup and
  undo; View and Manage permissions; works on the stock panel and with themes.
