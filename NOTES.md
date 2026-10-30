---
tags:
  - fork-ledger
  - caelestia
---

# NOTES.md — caelestia — the repo decision log

One card per decision/commit, oldest first — append new cards at the bottom.
Cross-repo cards live in the global `../NOTES.md`; empty slots stay bare, no filler.

## 2026-10-30 22:54
* **What:** Upstream sync — `main` fast-forwarded `f4bb062` → `d4c24f86` (5 commits / 7 files) and catch-up-merged into `custom` (`2c98623`, pushed). `custom` now differs from `main` only by our five doc files. Brings: the **breaking** Hyprland `lock_active()` → `lock()` replacement (#535), the `specialWsCloseAny` option (#516), silent workspace-move keybinds (#512) and a picture-in-picture matching fix (#533)
* **Why:** catch the base up with upstream — #535 removes a Hyprland call that upstream had deprecated and that breaks on newer Hyprland. These dot changes stay inert on the owner's machine until R-002 points `caelestia update` at this fork
* **Taught:** merge-base drift, catch-up merge, upstream-first porting
