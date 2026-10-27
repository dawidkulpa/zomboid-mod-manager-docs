---
title: "Applying, history and undo"
parent: "Features"
nav_order: 5
---

# Applying changes, history and undo

## The apply dialog

**Apply changes** opens a summary of the staged changes (added, removed, enabled, disabled, reordered) and two
choices:

- **Back up the game data first**: on by default (see
  [configuration.md](../configuration.md#back-up-before-changes-by-default)). The backup contains the game's data
  folder only: the world, the players and the server settings, without the game install and the downloaded
  Workshop files, which the server downloads again. The note below it names the folder and shows how many
  backups the server has and that the oldest unlocked one is removed when the limit is reached. Disabled when the
  server's backup limit is 0 or the user may not create backups.
- **Start the server when done** (**Start the server again** if it is running): off by default. Leave it off to keep
  adding mods while the server is stopped.

Both choices are remembered in the browser. If the server is running, the dialog warns that it will stop, and with
a backup chosen that it stops first and the backup runs while it is stopped.

Before anything happens, the panel checks the config on the server again. If someone changed the mod list since the
page was loaded, the apply is refused right away ("The mod list changed on the server since you loaded it") and the
server is not touched: reload the page and apply again. The same happens when the panel would refuse the backup (its limit of
backups per few minutes, or a full server whose backups are all locked): the dialog says why, and you can try later
or apply without a backup.

## What happens

The apply runs on the panel as a queued job, so closing the browser does not stop it:

1. **Stopping the server** if it runs, and waiting until it is offline. The game saves the world and rewrites its
   config when it shuts down, so the backup and the change come after that.
2. **Creating backup** (if chosen), while the server is stopped, so it holds the world exactly as the game saved it.
   The job waits until the panel reports the backup finished.
3. **Saving the mod list**: the panel checks that the server is still stopped, reads the config again and changes
   only the `WorkshopItems=`, `Mods=` and `Map=` lines. Every other byte, including line endings, stays as it was.
4. **Starting the server** if chosen.

Progress is shown step by step to everyone who can see the Mods page. Panel activity records the stop, the backup,
the file write and the start under the user who applied.

The server stays stopped while the backup runs. A large server can take minutes to back up; the progress shows
**Creating backup** meanwhile.

The apply does not depend on the browser or on anyone opening the Mods page: if the panel's queue worker restarts
in the middle, the panel's scheduler picks the apply up again within a few minutes. This needs the panel's scheduler
(the `schedule:run` cron entry every Pterodactyl panel has).

## When something fails

When an apply fails before the mod list was saved, your mods are not changed. If the apply had stopped the server,
it starts the server again and the message says so ("The server was stopped for this change and has been started
again"); if the server cannot be started, the message says it is still stopped.

- **Backup failed**: your mods were not changed. **Try again**, or **Apply without backup**.
- **The server's node stopped answering**: the panel retries for two minutes before giving up.
- **The server was started while the change was applied**: someone started the server during the backup. Nothing
  is written to a running server; apply again.
- **The mod list could not be saved**: the file on the server may be incomplete. The server is left stopped; check
  the file before starting it.
- **Server didn't start**: the mod changes are saved; check the console before starting again.
- A user without permission to stop the server cannot apply while it runs. If the server was offline when they
  applied and someone starts it before the apply stops it, the apply ends without stopping it: "The server was
  started meanwhile, and you don't have permission to stop it."
- If the node reports a power state the panel does not know, the server counts as running.

## History and undo

The **History** tab lists every applied change, newest first, with the user, the time and the backup made before
it. **Undo** opens the apply dialog as **Undo changes** with the reverse change (the mod lines as they were before
that entry), so it is reviewed and applied like any other change, with its own backup and history entry.

Undo restores the mod lines only. To restore world data, restore the listed backup in the server's **Backups** tab.
