---
title: "Missing requirements"
parent: "Features"
nav_order: 3
---

# Missing requirements

A mod can require other mods (`require=` in its `mod.info`). If an enabled mod requires one that is not enabled, it
will not load properly. The extension lists each case with a fix. Fixes are staged like any other change.

## Where they show

- On the item's row: **N missing requirements**. Click it to open the list.
- The **Problems** filter shows only items with problems, with a summary on top.
- The **Load order** tab marks the same mods, with **Fix in Installed**.

Each entry reads like `TombBodyCompatBootsExp needs SM4BootsExpandedB42`.

## Fixes

| Case | Actions |
| --- | --- |
| The required mod is on the server but turned off | **Turn on _mod_** (it loads right before the mod that needs it), or **Turn off _needing mod_** |
| Likely a compatibility patch for a mod you don't have | **Turn off this patch**, or **Find on Workshop** |
| The required mod is not on the server | **Find on Workshop**, or **Turn off _needing mod_** |

**Likely patch** means: the mod needs something no installed item has, it sits in a Workshop item whose other
mods work, and no working mod needs it. Project Zomboid has no "patch" flag, so this is inferred from that structure,
never from names, hence "likely". Turning it off breaks nothing that works now.

On the **Problems** filter, **Turn off N likely patches** does all of them in one change.

## Find on Workshop

Needs a Steam Web API key. Steam cannot search by mod ID, so the extension searches the Workshop for the ID and
shows up to three items whose description names it on a `Mod ID:` line, Build 42 items first. **Add** also adds
the item's own requirements. If nothing matches, **Search Workshop for _ID_** opens the Browse tab.

Forks and modpacks sometimes use the same ID: check the author and subscribers before adding.
