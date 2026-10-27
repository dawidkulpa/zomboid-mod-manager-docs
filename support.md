---
title: Support
nav_order: 5
---

# Support

Questions, bug reports and feature ideas are welcome. Contact the author in either place:

- **BuiltByBit**: send a message to the author of Zomboid Mod Manager on BuiltByBit.
- **Discord**: send a direct message to **buggy121**.

## What to include

It speeds things up a lot when a report has:

- the extension version (`php artisan p:extension:list` shows it), the panel version and the Wings version;
- the Project Zomboid build of the server (Build 42 only is supported);
- what you did, what you expected, and what happened, with a screenshot of the Mods page or the error message;
- for apply problems: the step it stopped at and the time, from the **History** tab or the progress view.

## Never send

Do not send your Steam Web API key, the panel's `APP_KEY` or `.env`, Wings configuration or tokens, or passwords.
Nothing in a report needs them. If a log you want to share contains one of them, remove it first.

## Before you ask

- No **Mods** tab on a server: see [Which servers get the Mods page](installation.md#which-servers-get-the-mods-page).
- An apply that never finishes: the panel's queue worker and scheduler must be running, see
  [Requirements](installation.md#requirements).
- Workshop search says the key is missing or refused: see [Steam Web API key](configuration.md#steam-web-api-key).
