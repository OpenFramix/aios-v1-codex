---
name: level-up
description: Use monthly (minimum) to find and ship one new automation. Walks the OFX Blueprint interview — Mindset (find the candidate) → Method (scope one) → Machine (build it). Trigger on "/level-up", "let's level up", "what should I automate next", "find me leverage this month", or any time a manual task surfaces mid-retainer. One run = one shipped artifact.
---

# /level-up — Monthly automation build

Execute the full level-up skill defined in this repo at `.claude/skills/level-up/skill.md`.

## What to do

1. Read `.claude/skills/level-up/skill.md` in full.
2. Follow every step in that file exactly — open with the candidate pipeline from `context/candidates.md`, run the stale-automation check (per `.claude/rules/change-management.md`) and the orphaned-automation check before Phase 1, then walk Mindset → Method → Machine, ship exactly one artifact, write the tracking file in `tracking/`, and update `context/candidates.md`.
3. One run = one artifact. Never ship more than one per session.
4. Honor `CLAUDE.md` and every rule in `.claude/rules/` before producing client-facing output.

## Why a thin wrapper

The skill logic lives in `.claude/skills/level-up/skill.md` so it stays editable as the AIOS evolves per-client. This plugin entry only registers the command in Cowork's palette and points Claude at the live skill file.
