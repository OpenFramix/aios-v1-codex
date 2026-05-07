# aios-v1 — OpenFramix AI Operating System plugin

Six core skills that turn an AIOS repo into a working operating system inside Claude Cowork.

## What it does

This plugin registers the six AIOS skills as native Cowork commands. The skill logic itself lives in `.claude/skills/` in the AIOS repo — this plugin is a thin wrapper that surfaces each skill in Cowork's command palette and points Claude at the live skill file when invoked.

The skills stay editable per-client. The plugin stays the same across every install.

## Commands

| Command | When to run | What it does |
|---|---|---|
| `/onboard` | Day 1 | Reads the intake, researches the industry, scaffolds all context files, generates the initial candidate pipeline. Idempotent — re-run any time the intake is updated. |
| `/audit` | Day 7, then monthly | Five-layer scoreboard out of 100 with the top-3 fixes ranked by leverage. Structural — "is the AIOS built right?" |
| `/level-up` | Monthly minimum | Walks the OFX Blueprint — Mindset → Method → Machine — and ships exactly one new automation per run. |
| `/explore` | Start of each month or after a new connection is wired | Re-ranks the candidate pipeline by what's buildable now. Discovery-only — does not build. |
| `/morning-brief` | Daily | Today's agenda, tasks, overnight activity, one focus. Readable in 60 seconds. |
| `/roi-report` | End of each retainer month | One-page client-facing report — automations run, time saved, AIOS health score, what's queued. The retainer renewal argument. |

Plain-English equivalents also trigger each skill — "run my morning brief", "let's level up", "audit my setup", "explore what I should build", "generate my ROI report", "onboard me".

## How it works

Each skill in this plugin is a thin SKILL.md wrapper with frontmatter for the Cowork command palette and a body that instructs Claude to read and execute the corresponding file in `.claude/skills/<name>/skill.md`.

This means:

- Per-client edits to a skill's logic happen in `.claude/skills/<name>/skill.md` and take effect immediately
- The plugin doesn't need to be re-published when a skill is tuned
- Voice, brand, and rule files in the AIOS repo are honored automatically because the skill logic reads them

## Install

1. Clone the AIOS repo for the client (`aios-v1`)
2. Open the cloned folder in Claude Cowork
3. Install this plugin from `.cowork/aios-v1.plugin`
4. All six commands appear in the Cowork palette

The plugin file ships in the repo, so every future client install picks it up automatically.

## Repo layout this plugin expects

```
<repo root>/
├── CLAUDE.md                       # Operating manual — read every session
├── .claude/
│   ├── rules/                      # Always-on passive rules
│   └── skills/
│       ├── onboard/skill.md
│       ├── audit/skill.md
│       ├── level-up/skill.md
│       ├── explore/skill.md
│       ├── morning-brief/skill.md
│       └── roi-report/skill.md
├── context/                        # Filled by /onboard
├── references/                     # Brand, voice, blueprint
├── connections.md
├── decisions/log.md
├── runs/
├── tracking/
├── audits/
└── .cowork/
    └── aios-v1.plugin              # This plugin
```

## Authoring

Built and maintained by **OpenFramix**.

To edit a skill's behavior, edit the corresponding file in `.claude/skills/<name>/skill.md`. To change a command's name, description, or trigger phrases, edit the matching `SKILL.md` in this plugin.

To bump the plugin version, update `version` in `.claude-plugin/plugin.json` and re-package.
