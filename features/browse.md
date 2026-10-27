---
title: "Adding mods"
parent: "Features"
nav_order: 2
---

# Adding mods

**Add mods** opens the **Browse Workshop** tab.

## By link or ID

No API key needed. **Paste link or ID** takes a Workshop link or a numeric ID; **Find item** shows it, then add it.

## Search

Needs a Steam Web API key.

- Search by name, author or tag. 30 results at a time; **Load next 30** for more.
- Sort by **Trending this week**, **Most popular**, **Top rated**, **Recently updated** or **Newest**. **Title**,
  **Size**, **Tags** and **Status** sort the loaded results.
- Filters: Workshop categories, **Works on Build 42**, **Hide translations**, **Hide installed**.
- **Grid** or **List** view.

## Item details

Click a title: screenshots, rating, subscribers, dates, size, description, tags and a link to the change notes.

- **Requirements**: the items it needs and whether you have them. **Add with N requirements** adds them all.
- **What this adds to the server**: for items with several mods, choose which to enable. Map folders are placed on
  the `Map=` line automatically.

## Import a collection

Needs a key. **Import collection** → paste the link or ID → untick what you don't want → **Add N items**. Lists up
to 1,000 items.

## Server's own key

When the admin [allows server keys](../configuration.md#steam-web-api-key-source) and the server has none, this tab
shows a **Steam Web API key** card to add one. Later, **Steam key** in the page header replaces or removes it.

## Limits

| Message | What to do |
| --- | --- |
| "Too many Workshop requests, try again in N s." | Wait, then **Retry**. Loaded results stay. |
| "Workshop search is paused until …" | The key's daily calls are used up. Adding by link or ID still works. |

All data comes from the official Steam Web API, called by the panel. The extension does not scrape Steam pages.
Added items are staged; [apply](applying.md) them.
