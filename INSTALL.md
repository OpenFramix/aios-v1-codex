# Installation Guide

One repo. One delivery target. Codex is the operating environment; the client-specific repo is the product.

## Clone the Client Repo

```bash
cd ~/Projects
git clone https://github.com/OpenFramix/aios-v1.git [client-name]-aios
cd [client-name]-aios
```

Use a private repo for each client install. The OS files are shared across installs; the context files become client-specific.

## Setup Sequence

**Step 1 — Fill the intake**

Open `aios-intake.md` and walk through Q1–Q10 with the client. Write answers directly into the file as you go. The better the intake, the sharper the candidate pipeline.

**Step 2 — Confirm the Codex structure**

The repo should have:

- `AGENTS.md` as the root operating manual.
- `.agents/skills/<name>/SKILL.md` for each core skill.
- `.agents/rules/` for always-on operating rules.
- `context/`, `references/`, `runs/`, `audits/`, `tracking/`, and `decisions/`.

**Step 3 — Run `/onboard`**

In Codex, type `/onboard`. The skill reads the intake, researches the industry, generates `context/candidates.md`, scaffolds the context files, builds `references/DESIGN.md`, and prepares the first connection sprint.

**Step 4 — Run `/audit`**

Type `/audit` to establish the baseline AIOS health score. Show the client the starting point and the highest-leverage next action.

**Step 5 — Wire Connection 1**

Based on the intake and candidate pipeline, wire the highest-leverage first connection. Update `connections.md` and add the relevant API/reference guide under `references/`.

**Step 6 — Configure recurring cadence**

Set up the morning brief through Codex app automations or the client access layer. The expected output is a dated file in `runs/`, such as `runs/morning-brief-YYYY-MM-DD.md`.

**Step 7 — Push the client install**

```bash
git remote set-url origin https://github.com/OpenFramix/[client-name]-aios.git
git add AGENTS.md .agents context connections.md references decisions runs audits tracking VERSION.md
git commit -m "Onboarding complete - [client name]"
git push origin main
```

## Client Use

The client works in the Codex-backed interface and asks naturally. Slash commands are available for the six core skills, and plain-English equivalents route through `AGENTS.md` when slash commands are not available.

## Updating Client Installs

Skills, rules, and framework references are OS-level. Push improvements deliberately:

```bash
# Add or update a skill in a client repo:
cp -R ~/Projects/aios-v1/.agents/skills/new-skill ~/Projects/[client-name]-aios/.agents/skills/
cd ~/Projects/[client-name]-aios
git add .agents/skills/new-skill
git commit -m "OS upgrade: add /new-skill"
git push
```

Client-specific files live in `context/`, `references/voice.md`, `references/DESIGN.md`, `connections.md`, `decisions/`, `runs/`, `audits/`, and `tracking/`. Do not overwrite those during OS upgrades unless the change is intentional.
