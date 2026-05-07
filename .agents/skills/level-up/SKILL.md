---
name: "level-up"
description: "Use monthly (minimum) to find and ship one new automation. Walks the OFX Blueprint interview — Mindset (find the candidate) → Method (scope one) → Machine (build it). Trigger on \"let's level up\", \"what should I automate next\", \"find me leverage this month\", or any time a manual task surfaces mid-retainer. One run = one shipped artifact."
---

## What this skill does

Walks the OFX Blueprint each month (minimum) to surface and ship one new automation. **One interview = one artifact.** It also installs the Blueprint into the client's thinking over time — after 4-6 runs, they start spotting opportunities mid-week without prompting because the questions have become internal defaults.

This is the compounding mechanism. The retainer delivers 1-2 automations per month — each one built through this process. Over a year, that's 12-24 systems running inside the business. The retainer grows because the AIOS grows.

## What `/level-up` is NOT

- Not `/audit`. `/audit` is structural ("is the AIOS built right?"). `/level-up` is functional ("what business leverage am I missing?"). Run `/audit` first if the structure is messy.
- Not `/explore`. `/explore` is discovery ("what should we build next?"). `/level-up` is delivery ("scope it and ship it"). Run `/explore` if the client doesn't know what they want. Run `/level-up` when they do.
- Not a multi-candidate planner. One run = one shipped artifact.

## When `/level-up` runs

- **First run: Day 14.** After at least one connection is wired and `/audit` has been run once. Earlier yields trivial output — the AIOS doesn't know enough yet.
- **Cadence: monthly minimum.** The retainer delivers 1-2 new automations per month — one `/level-up` per build. Weekly is ideal when the client is engaged and has flagged tasks mid-month. Monthly is the floor.
- **On-demand.** Any time a manual task surfaces mid-month or the client flags something worth building.

## Inputs the skill reads

- `context/priorities.md` — the client's 90-day priorities
- `context/about-me.md` — top pain, role
- `context/about-business.md` — offer, ICP, revenue model (Phase 1 candidates must connect to the business, not just the person)
- `context/domains.md` — the mapped business domains and tasks (start here when surfacing candidates)
- `connections.md` — what tools are reachable and by what mechanism
- `references/ofx-blueprint.md` — the OFX Blueprint framework reference
- `decisions/log.md` — what's already been scoped, shipped, or considered
- `.agents/skills/*/SKILL.md` frontmatter — what capabilities exist
- Most recent `audits/audit-{date}.md` if present — surfaces structural gaps to address

## Execution — three phases

### Phase 1 — Mindset: Find the Candidate

**Stale automation check — run this before anything else.** Read all files in `tracking/`. For any automation where `ramp-phase` is `1` and the `Built` date is 14+ days ago, surface them first:

> *"Before we find something new to build — [N] automation(s) have been at Training Wheels for 14+ days: [names and built dates]. Want to review advancement on any of these first?"*

If the operator says yes — walk through the advancement criteria (5+ confirmed runs, 2+ weeks) for each one. If both conditions are met, recommend the frontmatter edit and tracking file update. If the operator says no or `tracking/` is empty — move on.

**Learning capture check — run this second.** Scan `decisions/log.md` for any entries of type `Learning` filed since the last level-up session (check `runs/` for the most recent `level-up-{date}.md` to establish the cutoff date). If any exist, surface them before Phase 1 questions:

> *"Before we start — I captured [N] thing(s) worth noting since last month: [one-line summary per entry]. Want to start with one of these, or factor them into the candidate list?"*

If the operator wants to start with a captured item — skip directly to Phase 2 (Method) with that candidate. Mindset already happened in the background.
If the operator wants them factored in — weight them as top candidates during Phase 1. A real observed signal outranks a hypothetical from domains.md.
If no learning entries exist since last session — move on silently.

**Read `context/candidates.md` next.** Surface the top 3 entries where `Status: Ready to build`, sorted by Priority. Present them directly:

> *"Based on what I already know about your business, here are your top 3 highest-ROI moves ready to build right now:*
> *1. [Candidate name] — [ROI hypothesis]*
> *2. [Candidate name] — [ROI hypothesis]*
> *3. [Candidate name] — [ROI hypothesis]*
> *Which one, or is there something new you want to build instead?"*

If the client picks from the pipeline → skip the discovery questions entirely. Jump to Phase 2 with the chosen candidate.

If the client says "something new" → run the discovery questions below as a fallback. Also read `context/domains.md` before asking — candidates should connect to mapped domains.

**Discovery questions (fallback only — when client brings something new):**

1. *"Walk me through your week. What did you do 3 or more times?"* (frequency)
2. *"Anything that felt manual, boring, or copy-paste?"* (drudgery)
3. *"Anything where you thought 'someone else could handle this'?"* (delegation)
4. *"If 500 new clients showed up tomorrow, what would break first?"* (constraint)
5. *"What would bring 500 new clients if it ran on autopilot?"* (growth lever)

If a new candidate surfaces from these questions, add it to `context/candidates.md` (`Surfaced by: level-up`) before proceeding to Phase 2.

Reference OFX Blueprint principles when they fit naturally:
- *"The Lens: to what extent could AI be leveraged here? It's never binary — what percentage?"*
- *"Function Breakdown: you're not automating the whole job, just this one piece. Which piece?"*
- *"AI is better than you think and improving faster than you think. If it couldn't do this six months ago, it might be ready now."*

**Augmented vs. Automated framing** — before picking a candidate, clarify which type:
- **Augmented:** AI helps the human do the task faster (drafts, summaries, plans — human approves every step)
- **Automated:** AI handles it end-to-end without a human in the loop

Both are valid. Augmented is often the right place to start. Only push toward Automated if the task is well-understood and the augmented version has been validated first.

**Output of Phase 1:** numbered list of 1-3 candidates from `context/domains.md` and the conversation, one-line "why this is leverage" per candidate. Ask: *"Which one do you want to scope?"*

### Phase 2 — Method: Scope One

Client picks one. Walk the five-step Method pipeline:

**Step 1 — The Bottleneck.**
Which bottleneck does this solve, or which growth lever does it open? Tie it back to something in `context/priorities.md`. If it doesn't connect to a priority, ask: "Why is this worth building before [priority X]?"

**Step 2 — Three Gates.**
Every process goes through three gates in order:
- **Cut it first:** *"What happens if we just stop doing this entirely?"* If nothing breaks → exit cheerfully. Log it as a win in `decisions/log.md`. "We eliminated a task instead of automating it — that's better." Don't automate waste.
- **Automate it:** Apply The Mix 60-30-10 — ~60% fully automated, ~30% AI-assisted with human review, ~10% stays manual. Full automation is rarely the right target on the first build.
- **Hand it off:** If the task is too judgment-heavy or variable → suggest a person owns it. Exit with a delegation suggestion. Log it.

**Step 3 — Blueprint Process.**
Before touching any tool, map five elements. If the client can't answer all five, stop: *"If you can't explain this to a person, you can't explain it to AI. Sketch it on paper first, then come back."*

- **Trigger** — what kicks it off?
- **Data sources** — where does the information come from?
- **Transformations** — how does the data change shape?
- **Decision points** — where does it branch?
- **Destination** — where does the output go?

**Step 4 — Autonomy Ladder + Local vs. Remote.**

| Level | Name | What happens |
|---|---|---|
| L0 | Manual | No AI |
| L1 | Suggested | AI suggests, human decides every step |
| L2 | Drafted | AI drafts, human reviews and edits |
| L3 | Supervised | AI runs, human validates periodically |
| L4 | Autonomous | AI handles end-to-end |

**Default = lowest level that solves the problem.** Push back hard on L4 unless L1-L3 have been validated first. *"Workflows beat agents. If a decision doesn't have to be made by AI, don't let AI make it."*

Also ask: **Local or remote?**
- **Local** — needs files on the computer, a specific CLI tool, or the client's local apps. Runs on the VPS or Mac Mini. Requires the machine to be on.
- **Remote** — uses only Codex's native tools (web search, file creation). Can run in the cloud, machine can be off.

This determines how the automation gets deployed and whether it needs local scheduling or a Codex app automation.

**Step 5 — The Business Test.**
Which bucket does this move?
- More customers
- More value per customer
- Less cost

Plus a specific metric (response time, conversion rate, time saved, error rate). **If the client can't name a bucket and a metric, the skill stops.** *"If this automation doesn't move a number, why are we building it?"*

**Output of Phase 2:** write a scoped automation spec to `decisions/log.md` as a dated entry. Include: the candidate chosen, all five Blueprint Process answers, the autonomy level, local vs. remote, and the Business Test result.

### Phase 3 — Machine: Build It

Ask: *"How do you want to ship this?"* Options in Boring-is-Beautiful order:

1. **Prompt-only** — saved prompt template run manually. Zero infrastructure. Best starting point for anything judgment-heavy.
2. **Deterministic skill** — a `SKILL.md` that runs a script with no AI step. Best for transformations with clear rules.
3. **AI-assisted skill** — `SKILL.md` with one AI call. Drafts, classifies, summarizes.
4. **Sub-agent** — multi-step agent. Last resort. Only if the work genuinely requires reasoning + tool use across multiple steps.

**Default = highest non-AI option that solves the problem.** The client must explicitly choose more autonomy.

Once chosen, route to the skill creator if available, or write the `SKILL.md` inline with frontmatter, location, and full contents.

**Sub-skill consideration:** if the task requires multiple discrete steps (e.g., research + draft + send), build it as a parent skill that calls child skills in sequence. Each child does one job — One Job Rule. Don't build one monolithic skill for a complex workflow.

**Every scaffolded artifact ships with this header:**

```markdown
---
name: {automation-name}
description: {one-line description — used for slash-command discovery and /audit Capabilities scoring}
ramp-phase: 1
ramp-note: "Phase 1 — Training Wheels. Run this manually and confirm the output before advancing."
---
```

`name` and `description` are required — without them the skill is invisible to slash-command discovery and won't score in the Capabilities layer of `/audit`.

This locks the client and the operator into Phase 1 of The Ramp on first build. Advances only by explicit edit after validation.

Reference these Machine principles when scaffolding:
- **Block by Block** — smallest possible steps, deterministic first
- **Test Steps** — validate each step before connecting to the next
- **Ship and Improve** — ship the working version, improve from real usage
- **Simple Wins** — if a rule-based script works, don't build an AI agent

**The Ramp — all four phases.** Every artifact starts at Phase 1. Advances only by explicit decision after validation:

| Phase | Name | What happens |
|---|---|---|
| 1 | Training Wheels | Run manually, operator confirms every output |
| 2 | Guided | AI drafts, operator reviews before it goes anywhere |
| 3 | Watched | AI runs, operator spot-checks periodically |
| 4 | Hands-Off | Fully autonomous — earned, not assumed |

Communicate this to the client: *"This goes live in Training Wheels. We run it, we confirm the output, then we advance it. That's not a delay — that's how reliable systems get built."*

**New Hire Rule — deployment checklist.** Before any automation touches live client data or external systems:
- Dedicated credentials or API key scoped to this task only (not the owner's personal account)
- Read-only access by default — add write permissions only when the task explicitly requires it
- Full audit trail — every run logged to `runs/`
- Never impersonates the owner (no emails sent from the owner's personal address without explicit L3+ validation)

**Curiosity Rule — before closing Phase 3.** Don't accept the first output. Run it once, review the result, then ask: "What could go wrong here? What's an edge case this misses?" Test at least one edge case before marking the artifact ready. Ship and Improve means ship the validated version — not the first draft.

### Update `context/candidates.md`

After building the artifact, mark the corresponding candidate in `context/candidates.md` as built:

Find the entry matching the automation that was just built. Update the `Built:` field:
```
Built: YYYY-MM-DD
```

Do not delete the entry — mark it built so the pipeline shows accurate history and `/roi-report` and `/explore` can read it correctly. If the candidate came from a new "something new" conversation (not from the pipeline), add it as a new entry and immediately mark it built.

### Writing the output to `runs/`

After completing the session, write a timestamped summary to `runs/level-up-{YYYY-MM-DD}.md`:
- What candidate was surfaced
- What was scoped (Blueprint Process answers)
- What was built (skill/prompt/agent name and location)
- The Business Test result
- The Ramp phase it shipped at

This feeds the monthly ROI report.

### Creating the tracking file

After writing to `runs/`, create `tracking/{automation-name}.md` (using the automation's skill/artifact name, lowercased and hyphenated):

```markdown
---
ramp-phase: 1
domain: {domain from context/domains.md}
built: {YYYY-MM-DD}
---

# Tracking: {Automation Name}

**Estimated time per run:** {X minutes — how long this task took manually}
**Business Test bucket:** {More customers / More value per customer / Less cost}
**Metric:** {specific metric from the Business Test}

## Notes

{Leave blank — add notes as the automation runs and you learn from it}
```

The `ramp-phase` frontmatter field is what the stale check and change-management rule read. Always use frontmatter for this field — never body markdown. Update it here whenever the operator advances the phase.

Ask the client: *"How long did this task take you manually? That's the time-saved estimate."* Set it from their answer. If they don't know, use 15 minutes as the conservative floor and note it.

This file is read by `/roi-report` each month to calculate total time saved. Without it, the ROI report falls back to conservative estimates.

## Output contract

Every `/level-up` run produces:

1. **One `decisions/log.md` entry** — the scoped Method spec
2. **One scaffolded artifact** — prompt, skill, or agent file with `ramp-phase: 1` header
3. **One `runs/level-up-{date}.md` entry** — for ROI tracking
4. **One `tracking/{automation-name}.md` file** — time estimate and metadata for the ROI report
5. **A one-screen close** — printed at the end of every run:

```
✓ Level-up complete — {date}

Scoped:       {candidate name and domain}
Built:        {artifact type} → {file path}
Business Test: {bucket} — metric: {specific metric to track}
Ramp Phase:   1 — Training Wheels

Next step: run it manually, confirm the output, then advance to Phase 2.
Next level-up: {suggested timing — "when this has run 5+ times" or specific date}
```

## Critical implementation rules

1. **One interview = one artifact.** No parallel scoping.
2. **Mindset phase always runs first.** Even if the client comes in with a pre-formed idea — run the Phase 1 questions anyway. They often find something better.
3. **Read domains.md before asking Phase 1 questions.** Candidates should connect to mapped domains.
4. **Three Gates enforces Cut first.** If Cut is the answer, exit with energy — eliminating a task is better than automating it.
5. **Default to lowest autonomy level.** Push back on L4 every time.
6. **Simple Wins default in Phase 3.** Default = highest non-AI option.
7. **Business Test is mandatory.** If the client can't name a bucket and a metric, stop.
8. **The Ramp ships into every artifact.** `ramp-phase: 1` in frontmatter, no exceptions.
9. **New Hire Rule on every deployment.** Scoped credentials, read-only by default, no impersonation, full audit trail.
10. **Curiosity Rule before closing.** Test at least one edge case before marking the artifact ready.
11. **Write to `runs/`.** Every session produces a timestamped output file.
12. **Create the tracking file.** Every built automation gets a `tracking/{name}.md` with the time estimate. No exceptions — this is the ROI report's data source.
13. **Read-only on all files except `decisions/log.md`, the new artifact, `runs/`, and `tracking/`.** Don't modify intake, context files, or existing skills.

## Verification (for the implementer)

- **Cold run.** No pre-formed idea. Skill reads domains.md, surfaces 2-3 candidates from mapped domains. Generic output ("you should build a brief") = fail. Candidates must reference specific domain tasks.
- **Cut-first test.** Feed a candidate that should be eliminated. Expected: skill suggests Cut, exits, logs the win as a decision.
- **L4 pushback test.** Client asks for a fully autonomous email-replier on the first build. Expected: skill insists on L1/L2 first, explains The Ramp, won't ship L4 without explicit override.
- **Simple Wins test.** Candidate is solvable with deterministic Python. Expected: skill recommends prompt-only or deterministic skill as default.
- **Ramp anti-skip.** Client asks to skip Training Wheels immediately. Expected: skill explains what each phase means and asks them to confirm they've validated lower phases.
- **Business Test stop.** Client can't name a bucket and a metric. Expected: skill stops Phase 2 and asks the question again before proceeding.
