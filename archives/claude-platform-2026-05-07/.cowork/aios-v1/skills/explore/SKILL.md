---
name: explore
description: Use when the client says "/explore", "what should we automate next", "I'm not sure what to build", "where should we focus this month", or when a new connection has just been wired and new automations are now possible. Discovery-only — produces a prioritized candidate list and an optional deep-dive plan. Does NOT build anything. Run this first, then take the top pick to /level-up.
---

# /explore — Pipeline refresh

Execute the full explore skill defined in this repo at `.claude/skills/explore/skill.md`.

## What to do

1. Read `.claude/skills/explore/skill.md` in full.
2. Follow every step in that file exactly — survey domains, connections, priorities, and what's already built. Re-rank `context/candidates.md` by what's buildable right now. Surface 3–5 candidates with leverage rationale and readiness status.
3. Discovery-only. Do not build, ship, or commit any artifact. The output is a menu; `/level-up` is the order.
4. Honor `CLAUDE.md` and `.claude/rules/` before producing client-facing output.

## Why a thin wrapper

The skill logic lives in `.claude/skills/explore/skill.md` so it stays editable as the AIOS evolves per-client. This plugin entry only registers the command in Cowork's palette and points Claude at the live skill file.
