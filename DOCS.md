# DOCS.md — the story of the caelestia fork
Non-coder-friendly first, "For devs" inside each chapter. See ../playbooks/docs-fold.md.
`Last folded: 2026-10-30 22:54 — upstream sync`

## **Chapter 1 — Upstream sync (2026-10-30)**
**What it is.** The dotfiles repository was brought back level with upstream: 5 new upstream commits (7 files) were merged into this repo's `custom` branch. The fork adds no code of its own yet — only documentation — but the Hyprland configuration underneath gained a handful of upstream changes.

**Why it exists.** These dots are what actually lands on your machine: the `caelestia` cli clones this repo and copies its files into `~/.config`. While the fork was parked on an October 13 snapshot, upstream fixed a Hyprland API that was being deprecated and added a few quality-of-life keybinds. Catching up means your dotfiles stay compatible with current Hyprland — and because upstream owns these files, syncing is far safer than hand-patching them.

**How it works (non-coder version).** `main` stays a pure copy of upstream and is never edited; `custom` is the branch that gets deployed to your machine. The sync slid `main` forward, merged it into `custom` as one labelled commit, then pushed to GitHub. (Nothing reaches your machine yet — that needs R-002, see below.)

**For devs.** Merge commit `2c98623`; upstream range `f4bb062..d4c24f86`. Changed files: `hypr/hyprland/execs.lua`, `hypr/hyprland/keybinds.lua`, `hypr/utils/functions.lua`, `hypr/variables.lua`. #535 is **breaking** — `lock_active()` → `lock()` (Hyprland removed the old call). #516 adds `specialWsCloseAny`; #512 adds silent workspace-move keybinds; #533 fixes picture-in-picture matching.

**How it differs from upstream.** Only the five fork documentation files (`AGENTS.md`, `CLAUDE.md`, `DOCS.md`, `NOTES.md`, `VERSIONS.md`). Upstream touches none of them, so future syncs should stay conflict-free.

**Risks / how to undo.** #535 is a breaking change: on a Hyprland version that still expects `lock_active()`, the lock keybind may do nothing or error — verify in the VM. Undo is `git revert -m 1 2c98623`, a normal commit; history is never rewritten. Bigger caveat: none of these dot changes affect your desktop until `caelestia update` is pointed at this fork (roadmap R-002).

**What was verified, and what wasn't.** Verified: fast-forward clean, `git merge-tree` conflict preview clean, `custom` contains upstream's tip, `diff main..custom` shows only the five doc files, zero conflict markers, local == GitHub. **Not verified:** that the lock keybind works, that the new keybinds behave, or that the dots deploy correctly — all HUMAN-ONLY in the VM (`playbooks/vm-verify.md`), still open as P0-6.

**You learned:** *merge-base drift*, *catch-up merge*, *upstream-first porting* (see the global Toolbox in `../DOCS.md`).
