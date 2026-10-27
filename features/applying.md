---
title: "Applying, history and undo"
parent: "Features"
nav_order: 5
---

# Applying, history and undo

## The apply dialog

**Apply changes** shows what will change and two options, both remembered in the browser:

- **Back up the game data first** (default from [settings](../configuration.md#back-up-game-data-before-applying-changes)):
  world, players and server settings, without the game install and Workshop downloads. The note shows the server's
  backup count; at the limit the oldest unlocked backup is deleted.
- **Start the server when done**: off by default, so you can keep editing while the server is stopped.

A running server is stopped for the change; the dialog warns about it.

The apply is refused before anything happens if the mod list on the server changed since the page loaded (reload and
apply again) or if the panel would refuse the backup (try later, or apply without a backup).

## Steps

1. **Stopping the server**, if it runs. The game saves the world and its config on shutdown.
2. **Creating backup**, if chosen, while the server is stopped. Large servers take minutes.
3. **Saving the mod list**: only the `WorkshopItems=`, `Mods=` and `Map=` lines change.
4. **Starting the server**, if chosen.

Everyone with access to the Mods page sees the progress. The apply runs as a queued job on the panel: closing the
browser does not stop it, and if the queue worker restarts, the scheduler resumes it within minutes. The panel's
activity log records each step under the user who applied.

## When something fails

If an apply fails before the mod list is saved, your mods are unchanged, and a server the apply stopped is started
again.

| Message | What to do |
| --- | --- |
| Backup failed | **Try again**, or **Apply without backup**. |
| The server's node stopped answering | The panel already retried for two minutes. Check the node, then apply again. |
| The server was started while the change was applied | Someone started it during the backup; nothing was written. Apply again. |
| The mod list could not be saved | The file may be incomplete. The server stays stopped; check the file before starting it. |
| Server didn't start | The mods are saved. Check the console. |
| The server was started meanwhile, and you don't have permission to stop it | Ask someone who can stop the server, or apply while it is offline. |

## History and undo

The **History** tab lists every applied change, newest first, with the user, time and the backup made before it.

**Undo** opens the reverse change in the apply dialog, with its own backup and history entry. It restores the mod
lines only; to restore the world, restore the listed backup in the server's **Backups** tab.
