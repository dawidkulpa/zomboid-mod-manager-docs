---
title: "Permissions"
parent: "Features"
nav_order: 6
---

# Permissions

The server owner and admins can do everything. Subusers get access in the server's **Users** tab, group
"Project Zomboid mods":

| Permission | Allows |
| --- | --- |
| **View** (`ext.zomboid-mods.view`) | See the Mods page: installed mods, load order and history. |
| **Manage** (`ext.zomboid-mods.manage`) | Add, remove, enable and reorder mods, and apply the changes. Includes View: a subuser with only Manage sees the Mods tab, the page and the progress of every apply. When the administrator lets servers use their own Steam Web API key, also add, replace and remove the server's key (it can never be read back). |

Applying also performs core actions, so a subuser needs the matching core permissions too:

| Action during apply | Core permission |
| --- | --- |
| Backup first | **Create backups** (`backup.create`) |
| Stopping a running server | **Stop server** (`control.stop`) |
| Starting the server when done | **Start server** (`control.start`) |

In the apply dialog, **Back up the game data first** and **Start the server when done** are disabled with an
explanation when the user lacks the permission. Without **Stop server**, a running server cannot be changed: the
dialog says so.

## View-only users

A user with View only sees the page read-only: no **Add mods**, no switches, no reordering, no **Undo**, and a note
"You can view mods but not change them." When the server needs its own Steam Web API key and has none, the note adds
"Ask the server owner to add a Steam Web API key". The panel checks permissions on every request, so changes sent directly to
the API are refused as well (HTTP 403).

The Mods page and its API exist only on Project Zomboid servers: servers whose egg has the tag `project-zomboid`, or
whose startup command runs the game's server (see [installation.md](../installation.md#which-servers-get-the-mods-page)).
Other servers answer 404.
