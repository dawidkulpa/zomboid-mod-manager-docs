---
title: "Performance"
parent: "Features"
nav_order: 7
---

# Performance

The Mods page is built for servers with hundreds of mods.

- **Long lists render only what is visible.** The installed list and the load order keep a few rows around the
  viewport in the page, whatever the number of mods. Measured on a test server with 345 Workshop items and 413 mods:
  scrolling both lists produced no browser task longer than 50 ms.
- **Images load lazily.** Previews and Workshop cards load as they come near the viewport; cards far below are not
  fetched.
- **No polling of its own.** The progress of an apply or a scan is followed through the panel's job-progress
  service only while that job runs; an idle page makes no requests. Steam data is fetched when a tab or dialog
  needs it and cached on the panel.
- **Small pages from Steam.** Search and browse load 30 results at a time.
- **Light on Wings.** The installed list is cached per Workshop item; only new or changed items are read again.
- **Calm motion.** Animations use only transform and opacity and respect the system's reduced-motion setting.
