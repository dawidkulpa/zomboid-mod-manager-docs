---
title: "Performance"
parent: "Features"
nav_order: 7
---

# Performance

Built for servers with hundreds of mods.

- Long lists render only the visible rows. Tested with 345 Workshop items and 413 mods: no browser task over 50 ms
  while scrolling.
- Images load as they scroll into view.
- An idle page makes no requests. Progress is followed only while an apply or scan runs.
- Steam results come 30 at a time and are cached on the panel.
- The installed list is cached per item, so Wings reads only new or changed items.
- Animations respect the system's reduced-motion setting.
