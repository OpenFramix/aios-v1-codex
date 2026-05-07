---
name: morning-brief
description: Use each morning to generate a daily brief — today's agenda, tasks due, overnight automation activity, and one focus recommendation. Trigger on "/morning-brief", "run my morning brief", "daily brief", or any scheduled morning run. Designed to run on a schedule. Connection-aware — quality scales with what's wired. Readable in 60 seconds.
---

# /morning-brief — Daily brief

Execute the full morning-brief skill defined in this repo at `.claude/skills/morning-brief/skill.md`.

## What to do

1. Read `.claude/skills/morning-brief/skill.md` in full.
2. Follow every step in that file exactly — pull today's agenda, due tasks, overnight automation activity from `runs/`, and one focus recommendation tied to the 90-day priorities in `context/priorities.md`.
3. Write the brief to `runs/morning-brief-{YYYY-MM-DD}.md`. Apply branding from `references/brand.md` and voice from `references/voice.md` per `CLAUDE.md`.
4. Readable in 60 seconds. Not a report — a brief.

## Why a thin wrapper

The skill logic lives in `.claude/skills/morning-brief/skill.md` so it stays editable as the AIOS evolves per-client. This plugin entry only registers the command in Cowork's palette and points Claude at the live skill file.
