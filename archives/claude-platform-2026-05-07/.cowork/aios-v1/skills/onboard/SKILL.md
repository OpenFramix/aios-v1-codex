---
name: onboard
description: Use on Day 1 of an AIOS install, when someone says "set me up", "onboard me", "let's get started", "/onboard", or the intake form has just been filled. Combined wizard — processes the intake, researches the industry, generates the initial candidate pipeline, and scaffolds the full Day-1 file set. Idempotent — re-run any time after editing aios-intake.md.
---

# /onboard — AIOS Day 1 setup

Execute the full onboarding skill defined in this repo at `.claude/skills/onboard/skill.md`.

## What to do

1. Read `.claude/skills/onboard/skill.md` in full.
2. Follow every step in that file exactly — Step 0 (AI history check), Step 1 (read intake), Step 2 (interview if needed), Step 1.5 (industry research), Step 3 (scaffold all Day-1 files), Step 4 (closing wow-moment screen).
3. Honor every "Critical implementation rule" in that file — voice paste cannot be skipped, domain tasks must be specific, candidates.md is written first, one-shot scaffold, idempotent re-runs back up to `archives/`.
4. Also read and obey `CLAUDE.md` and the rules in `.claude/rules/` before producing any client-facing output.

## Why a thin wrapper

The skill logic lives in `.claude/skills/onboard/skill.md` so it stays editable as the AIOS evolves per-client. This plugin entry only registers the command in Cowork's palette and points Claude at the live skill file.
