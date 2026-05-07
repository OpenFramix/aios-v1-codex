---
name: roi-report
description: Use at the end of each retainer month to generate the client-facing ROI report. Trigger on "/roi-report", "generate my ROI report", "monthly client report", or "show me what we shipped this month". Reads runs/, tracking/, and audits/ to produce a one-page summary — automations run, time saved, AIOS health score, and what's queued next month. The report IS the retainer renewal argument.
---

# /roi-report — Monthly client report

Execute the full roi-report skill defined in this repo at `.claude/skills/roi-report/skill.md`.

## What to do

1. Read `.claude/skills/roi-report/skill.md` in full.
2. Follow every step in that file exactly — read `runs/`, `tracking/`, and `audits/` to compile the month's backward ROI (what ran, time saved, health score delta) and forward ROI (pipeline value, what's queued).
3. Apply branding from `references/brand.md` and voice from `references/voice.md` per `CLAUDE.md`. The report is client-facing — never expose the machinery.
4. One page. The retainer renewal argument with no call needed.

## Why a thin wrapper

The skill logic lives in `.claude/skills/roi-report/skill.md` so it stays editable as the AIOS evolves per-client. This plugin entry only registers the command in Cowork's palette and points Claude at the live skill file.
