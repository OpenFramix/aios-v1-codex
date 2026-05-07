---
name: audit
description: Use when someone asks for an AIOS audit, asks to score their setup against the OFX Architecture, says "/audit", "is my AIOS working", "audit my setup", or "find gaps in my AIOS". Produces a five-layer scoreboard out of 100 with the top-3 fixes ranked by leverage. Run on Day 7, then monthly.
---

# /audit — OFX Architecture gap report

Execute the full audit skill defined in this repo at `.claude/skills/audit/skill.md`.

## What to do

1. Read `.claude/skills/audit/skill.md` in full.
2. Follow every step in that file exactly — read (never write) the operating manual, context files, skills, agents, connections, decisions, and runs history. Score each of the five layers out of 20. Surface strengths and the top-3 leverage-weighted gaps with concrete next steps.
3. Scope is structural ("is the AIOS built right?"). Capability gaps belong to `/explore` and `/level-up` — do not conflate.
4. Honor `CLAUDE.md` and `.claude/rules/` before producing client-facing output.

## Why a thin wrapper

The skill logic lives in `.claude/skills/audit/skill.md` so it stays editable as the AIOS evolves per-client. This plugin entry only registers the command in Cowork's palette and points Claude at the live skill file.
