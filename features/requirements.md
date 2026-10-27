---
title: "Missing requirements"
parent: "Features"
nav_order: 3
---

# Missing requirements

A mod's `mod.info` can require other mods (`require=`). When an enabled mod requires a mod that is not enabled,
Project Zomboid will not load it properly. The **Installed** tab lists every such requirement and offers the fix that
fits it. Nothing changes on the server until you apply, like every other edit.

## Where they show

- The row of the Workshop item gets a label such as **2 missing requirements**. Click it to open the list.
- The **Problems** filter shows only items with problems and opens their lists. A summary line on top counts them,
  for example "2 items have 4 missing requirements".
- The **Load order** tab marks the same mods with "Needs X, which is not enabled · **Fix in Installed**"; the link
  opens the item on the Installed tab with its list open.

Each entry names the mod that needs something and what it needs, for example
`TombBodyCompatBootsExp needs SM4BootsExpandedB42`. One item can have several entries.

## The fixes

| Case | What it means | Actions |
| --- | --- | --- |
| The required mod is on the server but turned off | It is in an installed item, just not enabled | **Turn on _mod_** (loads it right before the mod that needs it), **Turn off _needing mod_** |
| Likely a compatibility patch for a mod this server doesn't have | Most likely a compatibility patch inside an item with several mods (e.g. "Boots Expanded" support in a body overhaul), while the item's other enabled mods are fine | **Turn off this patch** (turns off only that mod), **Find on Workshop** |
| The required mod is not on the server | No installed item has it | **Find on Workshop**, **Turn off _needing mod_** |

Project Zomboid has no "patch" flag, so this case is inferred from the item's structure, not from names or
descriptions: the mod requires a mod no installed item has, it shares its Workshop item with enabled mods that work,
and no working mod requires it. That is why the text says "likely". A mod that another working mod needs is never
treated as a patch, so turning these off does not break anything that works now; it only gives up a part that could
not load anyway. If the part adds content you want, use **Find on Workshop** instead.

### Turn off every likely patch

On the **Problems** filter, **Turn off N likely patches** turns off all patches of the second case in one edit.
The pending bar shows them as disabled mods; **Discard** brings them back.

### Find on Workshop

Steam has no index of mod IDs, so the extension searches the Workshop for the mod ID (top 10 results) and reads
each result's description. An item is shown only when its description names the ID on a **Mod ID:** line
(`Mod ID: guns93`, `ModID=guns93`, or one entry of `Mod IDs: a, guns93`). Up to three are shown, Build 42 items
first, with rating, subscribers, last update and Build 42/41 tags. **Add** works as on the Browse tab and also adds
the item's own required Workshop items.

Forks and server modpacks sometimes name the same ID; check the subscribers and the author before adding. When no
item confirms the ID, the dialog says so and **Search Workshop for _ID_** opens the Browse tab with that search.

The lookup runs only when you open it, never for the whole list, and the panel caches each ID for 24 hours. It
needs the Steam Web API key (see [../configuration.md](../configuration.md)); without a key the other fixes still work
and the summary explains how to add a key.

## Read-only users

Users with view permission only see the same lists and labels, without actions.
