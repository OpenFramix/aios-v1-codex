# BUSINESS Codex/AIOS V1

A repo-native Codex AI Operating System for small businesses. Installed and managed by OpenFramix operators to deliver custom AI systems, automations, and operational support.

## What this is

BUSINESS Codex/AIOS V1 is the core brain — operating manual, skills, rules, context, references, and tracking — that turns a cloned repo into a working AIOS for a client. It ships lean, then `/onboard` fills the business context during the setup session.

## What ships in this kit

**6 Codex skills:**
- `/onboard` — Day 1 setup. Reads the intake, researches the industry, scaffolds all context files, and generates the initial candidate pipeline.
- `/audit` — OFX Architecture gap report. Five layers, 100 points. Run Day 7, then monthly.
- `/level-up` — Monthly automation build. One run = one shipped artifact.
- `/explore` — Pipeline refresh. Re-ranks candidates by what is buildable now.
- `/morning-brief` — Daily brief. Agenda, tasks, overnight activity, one focus. Readable in 60 seconds.
- `/roi-report` — Monthly client report. The retainer renewal argument.

**5 always-on rules:**
- `business-scorecard` — watches for stalling domains, untracked metrics, and stale decisions.
- `change-management` — enforces ramp phase discipline on every automation.
- `continuous-learning` — captures automation signals during sessions.
- `decision-follow-through` — surfaces open commitments at the right moment.
- `opportunity-radar` — spots automation candidates from the domain map and connections.

**References:**
- `references/ofx-blueprint.md` — the OFX Blueprint framework: Mindset, Method, Machine.
- `references/DESIGN.md` — the brand source of truth for client-facing output.
- `references/gohighlevel-api.md` — GHL API reference, a common first connection.

## Install sequence

See `INSTALL.md` for the full Codex-native install sequence.

**Quick summary:**
1. Clone this repo for the client.
2. Set `{{operator_name}}` in `aios-intake.md` and `AGENTS.md ## Operator`.
3. Add an install row to `VERSION.md`.
4. Walk through `aios-intake.md` Q1–Q10 with the client.
5. Run `/onboard` to scaffold context, brand, and candidates.
6. Run `/audit` to establish the baseline score.
7. Configure the client access channel.
8. Wire Connection 1, usually GoHighLevel or Gmail.

## What to customize per client

`aios-intake.md`, `context/`, `references/voice.md`, `references/DESIGN.md`, and `connections.md` are generated or updated during `/onboard`.

## What stays as OS defaults

`AGENTS.md`, `.agents/skills/`, `.agents/rules/`, and `references/ofx-blueprint.md` are OS-level defaults. Do not customize skills or rules per client unless you are intentionally upgrading the OS.

## Version

V1.0.0 — see `VERSION.md` for install history.

---

*Everything AI. — OpenFramix*
