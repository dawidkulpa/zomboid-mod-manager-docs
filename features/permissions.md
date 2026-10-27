---
title: "Permissions"
parent: "Features"
nav_order: 6
---

# Permissions

The server owner and admins can do everything. Subusers get access in the server's **Users** tab, group **Project
Zomboid mods**:

| Permission | Allows |
| --- | --- |
| **View** | See installed mods, load order and history. Read-only. |
| **Manage** | Everything in View, plus add, remove, enable, reorder and apply. In the server-key modes, also set or remove the server's Steam key. |

Applying also needs these panel permissions for the matching steps:

| Step | Panel permission |
| --- | --- |
| Backup first | **Create backups** |
| Stopping a running server | **Stop server** |
| Starting the server when done | **Start server** |

Options the user lacks a permission for are disabled in the apply dialog, with the reason. Without **Stop server**, a
running server cannot be changed.

The panel checks permissions on every request, including direct API calls.
