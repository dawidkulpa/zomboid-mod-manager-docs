---
title: "Adding mods"
parent: "Features"
nav_order: 2
---

# Adding mods

**Add mods** opens the **Browse Workshop** tab. Mods can be added in three ways.

## Paste a link or ID (no API key needed)

**Paste link or ID** accepts a Workshop link (`https://steamcommunity.com/sharedfiles/filedetails/?id=…`) or the
numeric ID. **Find item** shows the item; add it from there. Clear messages appear when the item does not exist or
belongs to another game.

## Browse and search (needs a Steam Web API key)

- Search by name, author or tag. Results load 30 at a time; **Load next 30** fetches more.
- Sort: **Trending this week**, **Most popular**, **Top rated**, **Recently updated**, **Newest** (sorted by
  Steam), and **Title**, **Size**, **Tags**, **Status** (sorted on the loaded results).
- **Filters**: Workshop categories, **Works on Build 42**, **Hide translations**, **Hide installed**. Active filters
  show as chips; **Clear filters** resets them.
- **Grid** or **List** view; the choice is remembered in the browser.
- Each card shows preview, title, author, a short summary, rating, subscribers, tags, size and its status
  (installed, added, or **Add**).

Without a key this tab explains how to add one (admins) or to ask an admin (other users); adding by link or ID
still works. When the administrator lets servers use their own key ([configuration](../configuration.md#steam-web-api-key-source)),
the tab shows the **Steam Web API key** card instead: how to get a key, a field for it, **Save**. The key is checked
with Steam before it is saved. Later, **Steam key** in the page header replaces or removes it.

### Limits

The administrator limits real calls to Steam ([configuration](../configuration.md#steam-call-limits)); cached
results never count.

- Too many calls in a minute: "Too many Workshop requests, try again in N s." **Retry** after that; results already
  loaded stay.
- The key's calls for the day are used up: "Workshop search is paused until <time>." (00:00 UTC in your time zone).
  **Paste link or ID** keeps working.

## Details

Click a title for the details view: screenshots (arrow keys switch them), rating, subscribers, favourites,
created and updated dates, size, comments, a link to the change notes on Steam, the description and tags.

- **Requirements**: items this one needs, with their status. **Add with N requirements** adds them together.
- **What this adds to the server**: for items with several mods, choose which mods to enable. Map folders are listed
  and placed on the `Map=` line automatically.

## Import a collection (needs a key)

**Import collection** takes a collection link or ID and lists its items with their status. Uncheck what you do not
want and press **Add N items**. At most the first 1,000 items of a collection are listed; the dialog says so for a
larger one.

## Where the data comes from

Only the official Steam Web API (`api.steampowered.com`), called by the panel with the panel-wide key or the
server's own key. The extension does not load or scrape Steam Community web pages. Results are cached on the panel,
"not found" answers for an hour.

Added items are staged like any other change; apply them as described in [applying.md](applying.md).
