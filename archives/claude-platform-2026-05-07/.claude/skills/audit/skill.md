---
name: audit
description: Use when someone asks for an AIOS audit, asks to score their setup against the OFX Architecture, or says "is my AIOS working" / "audit my setup" / "find gaps in my AIOS". Produces a five-layer scoreboard with top-3 fixes ranked by leverage.
---

## What this skill does

Runs the **OFX Architecture Audit** on the current Claude Code project. Reads (never writes) the project's operating manual, context files, skills, agents, connections, decisions, and runs history. Scores each of the five layers out of 20. Surfaces strengths and the top 3 leverage-weighted gaps with concrete next steps.

**Scope is structural — "is the AIOS built right?"** It is NOT a capability planner. Capability gaps belong to `/explore` and `/level-up`. The audit answers: are the files, folders, registries, connections, and interfaces in good shape?

First run on Day 7 is the baseline. Re-run monthly to watch the score climb. The score report goes to the client as part of the monthly ROI report — it shows the AIOS getting stronger over time.

## Today's context

- **Date:** !`date +%Y-%m-%d`
- **Project root:** the current working directory

## The OFX Architecture — Five Layers (scored 20 each = 100 total)

| Layer | What it tests |
|---|---|
| **Context** | The AIOS knows the business — identity, voice, domains, decisions, references |
| **Connections** | The AIOS reaches the client's tools — APIs, MCPs, data sources |
| **Capabilities** | The AIOS knows how to do the work — skills organized by business domain |
| **Cadence** | The AIOS runs without being asked — scheduled triggers, active usage, run history |
| **Access** | The AIOS is usable without a terminal — interface, session management, non-technical access |

## Execution

### Step 1: Discover the project shape

Look for patterns and intent, not exact file paths. Names vary. Use Glob and Read to check:

**Operating manual:** `CLAUDE.md` (root), `CLAUDE.local.md` (gitignored)
**Context files:** `context/about-me.md`, `context/about-business.md`, `context/priorities.md`, `context/domains.md`, `context/tech-stack.md`
**Memory:** `MEMORY.md`, `memory/` folder, or equivalent
**Skills:** `.claude/skills/*/skill.md` — count + read frontmatter only
**Agents:** `.claude/agents/*.md` — count
**Connections:** `connections.md` (anywhere), `.env`, `.mcp.json`, `.claude/settings.json` (mcpServers), API scripts in `scripts/`, reference guides in `references/`
**Decisions:** `decisions/log.md` or any append-only decisions file
**References:** `references/` folder contents
**Runs history:** `runs/` folder — count files, check timestamps
**Tracking:** `tracking/` folder — evidence of ROI logging
**Interface:** Any mention of a dashboard URL, `dashboard/` folder, or interface project reference in CLAUDE.md
**Hooks/schedules:** `.claude/settings.json` hooks key, skill names matching `morning-*`, `daily-*`, `weekly-*`, `monthly-*`

Don't penalize for non-canonical names if equivalent intent is captured elsewhere.

### Step 2: Score each layer (20 points each)

---

#### Context (20 pts)

| Criterion | Points | How to detect |
|---|---|---|
| CLAUDE.md exists and is substantive (>200 words) | 4 | Read and count words |
| Core context files exist and are filled | 4 | `context/about-me.md`, `context/about-business.md`, AND `context/priorities.md` all exist with real content — not placeholders. Missing any one = 0. |
| `context/domains.md` exists and is populated | 4 | File exists with ≥2 named domains and tasks listed under each. Empty or placeholder = 0. |
| Voice reference exists | 4 | `references/voice.md` exists with verbatim writing samples (not typed mid-session). Any placeholder or empty file = 0. |
| Candidate pipeline exists and populated | 4 | `context/candidates.md` exists with ≥3 entries, at least 1 with `Status: Ready to build`. Empty or missing = 0. |

---

#### Connections (20 pts) — domain-aware, mechanism-agnostic

A "reachable" connection counts via ANY mechanism: MCP, API script, export pipeline, `.env` key + `references/{tool}-api.md`. No preference for MCPs — API scripts are equally valid.

**The 7 Tier-1 Business Domains:**

| # | Domain | Examples |
|---|---|---|
| 1 | Revenue / Financials | GoHighLevel, Stripe, Square, QuickBooks |
| 2 | Customer interactions | GHL CRM, Gmail-as-CRM, HubSpot |
| 3 | Calendar | Google Cal, Outlook, Calendly |
| 4 | Communication | Gmail, Outlook, Slack, text/phone noted |
| 5 | Project / task tracking | ClickUp, Notion, Asana, or even "tracked in a notebook" |
| 6 | Meeting intelligence | Granola, Otter, Fireflies, Zoom recordings |
| 7 | Knowledge / files | Google Drive, Dropbox, Notion, local folders |

Also check `context/tech-stack.md` — tools listed there but not yet in connections.md are gaps worth surfacing.

| Criterion | Points | How to detect |
|---|---|---|
| Tier-1 domain coverage | 8 | 1.15 pts per tier-1 domain reachable. Round to nearest 0.5. Cap 8. |
| Reference guide presence | 4 | -0.5 per connected tool with no `references/{tool}-api.md`. Floor 0. |
| Auth / pipeline freshness | 4 | -1 per connection marked `needs-auth`/`expired`, or script not run within 30 days. Floor 0. |
| `connections.md` documentation | 2 | 0 if missing; 1 if sparse; 2 if all reachable tools documented |
| Read-AND-write balance | 2 | ≥1 connection can WRITE (send message, post update, create record). 0 if all read-only — a viewer, not an OS. |

---

#### Capabilities (20 pts)

| Criterion | Points | How to detect |
|---|---|---|
| 3+ skills installed | 8 | Count `.claude/skills/*/skill.md` |
| 1+ user-built domain skill | 8 | Skill names NOT in the OFX canonical list below. If skill name maps to a domain in `context/domains.md`, it scores full points. If it exists but doesn't map to a domain, it still scores full points — the domain alignment is aspirational, not required. |
| 1+ agent defined | 4 | `.claude/agents/*.md` ≥ 1 |

**OFX canonical skills (don't count as user-built):**
`onboard`, `audit`, `level-up`, `explore`, `roi-report`, `morning-brief`, `skill-creator`, `skill-builder`, `decision`, `connect`, `connect-check`, `memory-prune`, `scaffold-skill`, `scaffold-agent`, `draft`, `standup`

---

#### Cadence (20 pts)

| Criterion | Points | How to detect |
|---|---|---|
| 1+ recurring/scheduled trigger | 8 | `runs/` contains output files from a scheduled skill (morning-brief, daily-*, weekly-*, monthly-*) = 8 pts. Skill exists but no run evidence yet = 4 pts. Neither = 0. Having the skill installed without run evidence does not prove it is scheduled. |
| Recent activity signal | 8 | `decisions/log.md` has an entry within the last 14 days, OR `runs/` has output files within the last 7 days. Skill modification timestamps alone do NOT count — they reflect install date, not usage. |
| Run history exists | 4 | `runs/` folder exists with ≥1 timestamped output file. If the folder doesn't exist, surface it as a gap — skills should be configured to write outputs here so the client can see what the AIOS produced. |

---

#### Access (20 pts)

| Criterion | Points | How to detect |
|---|---|---|
| Interface or dashboard documented and real | 8 | CLAUDE.md `## Interface` section describes: (1) a confirmed access method (iMessage/Telegram handle, or dashboard URL), AND (2) what the client can do without a terminal. Both required for full 8. URL/handle mentioned with real content = 4. Placeholder text only = 2. Missing entirely = 0. |
| Session management rules present | 6 | CLAUDE.md includes a vault-first memory rule (check files before answering), AND defines what happens at context limit (auto-compact behavior or session summary protocol) |
| Non-technical access demonstrated | 6 | Evidence the interface has actually been used: `runs/` contains a morning-brief file (proof it was delivered), OR the Interface section describes a confirmed channel with an active handle. If the section exists but is all placeholder = 2. If the section is filled with a real channel confirmed = 6. |

---

### Step 3: Identify top 3 gaps by leverage

For each criterion that lost points: leverage = (points lost) × (impact multiplier).

**Impact multipliers — if multiple rules match a gap, apply the highest multiplier only:**
- 0 tier-1 domains reachable: **4x** — AIOS is blind to the business
- CLAUDE.md missing or thin: **3x** — no foundation
- Core context files missing (about-me, about-business, priorities): **3x** — the AIOS doesn't know the business
- `context/domains.md` missing: **3x** — no blueprint for what to build
- `references/voice.md` missing: **3x** — every draft will sound wrong
- 1–2 tier-1 domains reachable (but not 0): **3x** — Connections is the gateway to live data
- 0 user-built skills: **2x** — no Capabilities = no AIOS
- No recurring trigger: **2x** — no Cadence = no autonomy
- All connections read-only: **2x** — viewer, not an OS
- No interface or session management: **2x** — unusable without the operator in the room
- 0 reference guides for connected tools: **1.5x**
- No decisions log: **1.5x**
- No run history: **1.5x** — no evidence the AIOS is doing anything
- All others: **1x**

Sort descending by leverage. Take top 3. For each, write one concrete next step:
- **Core context files missing:** "Edit `aios-intake.md` with the missing answers, then re-run `/onboard` to regenerate context files."
- **Domain map missing or thin:** "Edit `aios-intake.md` Q3 with specific business domains and named tasks, then re-run `/onboard` to regenerate `context/domains.md`. Vague domains like 'admin' don't count — need real task names."
- **Voice reference missing:** "Edit `aios-intake.md` Q2 with verbatim writing samples (from sent email or social post — never typed mid-session), then re-run `/onboard`."
- **Need a domain skill:** "Use the skill creator to build a skill for [highest-pain task from domains.md — read it and name the specific task]."
- **Need to reach a domain:** "Prefer API script: write `scripts/{tool}_api.py` + document at `references/{tool}-api.md`."
- **No runs folder:** "Create `runs/` and configure skills to write timestamped output files there — this is the ROI evidence trail."
- **No interface documented:** "Add a `## Interface` section to CLAUDE.md describing how the client accesses the system. Even a placeholder with the intended URL counts toward Access scoring."
- **No session rules:** "Add the vault-first memory rule and compact protocol to CLAUDE.md."
- **Need a recurring trigger:** "Add a hook to `.claude/settings.json`, or build a `daily-brief` skill the client runs each morning."

### Step 4: Output the report

Print directly in chat (Markdown):

```
# OFX AIOS Audit — {date}
**Score: {total}/100** — {stage}

Stage thresholds:
  0–39  → Stage 0: Foundation  (context is set, nothing is connected yet)
  40–69 → Stage 1: Built       (connected and capable, running on-demand)
  70–89 → Stage 2: Compounding (running autonomously, improving each month)
  90–100 → Stage 3: Autonomous (the AIOS runs the business without prompting)

## Scoreboard

Context        {bar}  {n}/20  {label}
Connections    {bar}  {n}/20  {label}
Capabilities   {bar}  {n}/20  {label}
Cadence        {bar}  {n}/20  {label}
Access         {bar}  {n}/20  {label}

(bar = # per 4pts; label = "Strong" ≥16, "Solid" 12-15, "Thin" 6-11, "Missing" <6)

## Strengths
- {1-3 bullets from highest-scoring criteria}

## Top 3 Gaps (ranked by leverage)
1. **{gap}** (–{pts} × {multiplier}x)
   → {concrete next step}
2. **{gap}** (–{pts} × {multiplier}x)
   → {concrete next step}
3. **{gap}** (–{pts} × {multiplier}x)
   → {concrete next step}

## Recommended next action
{single most leveraged thing to do before the next audit}

---
This audit scores structure only — is the AIOS built right?
For capability gaps (what could be built next), run /explore or /level-up.
```

### Step 5: Offer to save and add to ROI tracking

After printing, ask: "Save this audit to `audits/audit-{date}.md`?" If yes, write it (creating `audits/` folder if needed).

If a previous audit exists in `audits/`, compare scores and add a delta line to the report:
```
vs. last audit ({previous date}): Context +2, Connections +5, Capabilities 0, Cadence +4, Access +8 → total +19
```

This delta line goes into the monthly ROI report. The client sees their AIOS getting stronger over time.

## Notes

- **Read-only by default.** Never modify CLAUDE.md, context files, skills, or connections. Only writes: the audit report + `audits/` folder.
- **Be honest, not generous.** Stage 1 (40-69) is a good first-month score. Stage 3 takes real work. Don't inflate.
- **Domain map is load-bearing.** If `context/domains.md` is missing, the whole Capabilities layer is guesswork. Flag it with a 3x multiplier every time.
- **Access layer will score low early.** That's expected — the dashboard is Phase 2. The score still matters because it creates urgency to build it.
- **Speed matters.** Report in under 60 seconds. Read frontmatter only for skill files. Don't read full skill contents.
- **Cadence detection requires evidence.** Skill modification timestamps and skill names alone do not prove scheduled activity. Always look for actual run files in `runs/` before awarding scheduled trigger points.
