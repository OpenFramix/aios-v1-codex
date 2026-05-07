---
name: explore
description: Use when the client says "what should we automate next?", "I'm not sure what to build", "where should we focus this month?", or when a new connection has just been wired and new automations are now possible. Discovery-only — produces a prioritized candidate list and an optional deep-dive plan. Does NOT build anything. Run this first, then take the top pick to /level-up.
---

## What this skill does

Surveys the AIOS — domains, connections, priorities, what's already built — and surfaces 3–5 automation candidates the client could actually build right now. For each candidate: what it is, why it's leverage, how it would be built, and whether all the pieces are in place to start today.

**The output is a menu. `/level-up` is the order.**

Every month there's a gap between "I know I should be automating something" and "here's the specific thing we're building." `/explore` closes that gap in one session. The client ends with a ranked list and a clear top pick ready to hand to `/level-up`.

## What `/explore` is NOT

- Not `/level-up`. `/level-up` scopes and ships one automation end-to-end. `/explore` surfaces candidates. If the client already knows what they want to build — skip this, go straight to `/level-up`.
- Not `/audit`. `/audit` scores the AIOS structure. `/explore` looks at what to build on top of it.
- Not a replacement for the monthly call. It's the preparation for it — run it before the check-in, not instead of it.

## When `/explore` runs

- **Monthly start.** Beginning of the retainer month, before deciding what to build.
- **After new connections.** A new tool just got wired — what automations does that unlock?
- **After an audit.** The audit surfaced gaps in specific domains — what skills would fill them?
- **Client is stuck.** They know they want to automate something but can't name it.
- **Mid-month triage.** A manual task surfaced during the month and the client isn't sure if it's worth building.

## Inputs the skill reads

- `context/domains.md` — primary input. The domain map shows which parts of the business are unmapped or under-automated.
- `context/priorities.md` — 90-day priorities. Candidates that don't connect to a priority rank lower.
- `connections.md` — what tools are reachable right now. Only surface automations that are actually buildable with current connections, or flag what connection is needed first.
- `decisions/log.md` — what's already been explored, scoped, or built. Never re-suggest something already in the log.
- `.claude/skills/*/skill.md` frontmatter — what capabilities already exist. No point suggesting a skill that's already built.
- Most recent `audits/audit-{date}.md` if present — audit gaps are high-leverage explore targets.

## Execution — three phases

### Phase 1: Read the pipeline first

**Step 1A: Check `context/candidates.md`**

Read `context/candidates.md` first. If the file exists and has ≥3 entries:

- Filter for `Status: Ready to build` entries
- Check if any `Status: Waiting on [tool]` entries are now buildable — cross-reference against `connections.md`. If a required tool has since been wired, update that entry's status to `Ready to build` before surfacing.
- Re-rank by: Priority (High first) → connection readiness (Ready to build first) → time since surfaced (older surfaces first)
- Hold the top 3–5 for Phase 2

Ask: *"Anything new this month that should jump the queue before I show you what's already in the pipeline?"*

If the client says yes — hear it, add it as a new candidate entry in `candidates.md` (`Surfaced by: explore`), and include it in the Phase 2 ranking.

If `context/candidates.md` is missing or has fewer than 3 entries:
- Note: *"Your candidate pipeline is sparse — this usually means `/onboard` hasn't completed or needs a re-run. I'll surface what I can from your domains, but run `/onboard` first for best results."*
- Fall back to the cold survey below.

**Step 1B: Cold survey (fallback only)**

If candidates.md is missing or insufficient, build a picture from scratch:

Read `context/domains.md`. For each domain, note:
- Tasks marked as high automation potential with no corresponding skill or candidate
- Tasks described as recurring, manual, or copy-paste
- Domains with zero skills supporting them

Read `connections.md`. Note:
- Tier-1 domains wired but with no skill using that connection
- Any connection marked `needs-auth` or `expired` — flag as blocker, not candidate

Cross-reference `.claude/skills/` and `decisions/log.md`:
- Remove anything already built or scoped in the log
- Identify completely unserved domains

Audit gaps (if `audits/` exists):
- Read the most recent audit's Top 3 Gaps section
- Any gap with 2x or higher multiplier is a candidate

Learning captures:
- Scan `decisions/log.md` for `Learning` entries not yet acted on
- These are real observed signals — rank above hypothetical candidates from domains.md
- Flag with "(observed)" in the candidate list

After completing the cold survey, write any new candidates found to `context/candidates.md` using the standard format (`Surfaced by: explore`). Don't skip this write — every explore session should make the pipeline richer.

**The survey is silent.** Don't print status updates while reading files.

### Phase 2: Generate candidates

Surface 3–5 automation candidates. More than 5 creates decision fatigue. Fewer than 3 isn't a real choice.

**Ranking criteria (apply in this order):**
1. **Connection readiness** — can it be built today with what's wired? Buildable-now ranks first.
2. **Priority alignment** — does it support a stated 90-day priority?
3. **Leverage** — high-pain, high-frequency, or connected to a 2x+ audit gap
4. **Complexity** — simpler candidates rank higher at equal leverage (Simple Wins principle)

**For each candidate, surface:**

```
## Candidate [N]: [Specific name — not vague]

Domain: [which domain from domains.md]
Type: Augmented (AI helps human do it faster) / Automated (runs without human)
Status: Buildable now / Needs [connection name] first

Why this is leverage:
[One sentence tied to a specific pain, priority, or gap]

How it would work (rough):
- Trigger: [what starts it]
- Tools needed: [connections required — check against connections.md]
- Output: [what it produces and where it goes]

Estimated complexity: Simple (prompt-only or deterministic) / Medium (1 AI call) / Complex (multi-step)
Recommended starting point: L1 Suggested / L2 Drafted / L3 Supervised
```

**Hard rules:**
- Every candidate must name a specific task from `context/domains.md`, not a category. "Automate follow-ups" is not a candidate. "Send a follow-up text 24 hours after a GHL lead form submission" is.
- If a candidate needs a connection that isn't wired, label it `Needs [tool] first` — still surface it, but rank it below buildable-now candidates.
- Never suggest building a skill that already exists (check `.claude/skills/` frontmatter).
- Never suggest something already in `decisions/log.md`.

### Phase 3: Deep dive (optional)

After presenting the candidate list, ask:

*"Want me to deep-dive any of these before taking it to `/level-up`? Or is one of them clear enough to build now?"*

If the client picks a candidate for a deep dive:

Walk through the five Blueprint Process elements:

**Trigger** — what exactly kicks this off? An event in a connected tool? A time? A manual command?

**Data sources** — where does the input come from? Which connected tool? What format is the data in?

**Transformations** — what happens to the data? Reformatted, filtered, combined with other data, summarized?

**Decision points** — does it branch? Under what conditions does it do X vs. Y?

**Destination** — where does the output go? CRM record, email, Slack, file, dashboard?

If the client can't answer all five — stop. *"If you can't explain this to a person, you can't explain it to AI. Think it through first, then we'll scope it."* This is the same gate as `/level-up` Phase 2.

If all five are answered: write a brief spec to `decisions/log.md` as an explore entry (see format below). This pre-fills most of Phase 2 of `/level-up` — when the client is ready to build, the work is already half-done.

## Output contract

Every `/explore` run produces:

1. **A candidate list printed in chat** — 3–5 candidates in the format above
2. **An updated `context/candidates.md`** — new entries added, status changes applied, explored candidates marked as "discussed"
3. **A `decisions/log.md` explore entry** — candidate list summary + deep-dive spec if one was done
4. **A `runs/explore-{date}.md` entry** — for ROI tracking

**decisions/log.md explore entry format:**
```
## YYYY-MM-DD — Explore: [month or trigger]

**Candidates surfaced:** [N] candidates across [N] domains

**Top pick:** [candidate name] — [one-line why]

**Buildable now:** [list candidate names]
**Needs connection first:** [list candidate names + which connection]

**Deep dive completed:** [candidate name — or "none"]

[If deep dive was done, include Blueprint Process answers here]

**Recommended next action:** run /level-up on [candidate name]
```

**runs/explore-{YYYY-MM-DD}.md format:**
```
# Explore Run — YYYY-MM-DD

Candidates surfaced: [N]
Domains covered: [list]
Top pick: [candidate name]
Deep dive: [yes/no — candidate name]
Status: [handed to /level-up / pending client decision]
```

## One-screen close

Print at the end of every run:

```
✓ Explore complete — {date}

{N} candidates surfaced across {N} domains.

Top pick:     {candidate name} ({domain}) — {one-line why}
Status:       {Buildable now / Needs [connection] first}

Next step: run /level-up on "{candidate name}" to scope and build it.
```

## Critical implementation rules

1. **Discovery only.** Never build anything during `/explore`. No skill files, no scripts. The output is a plan, not a product.
2. **Survey silently.** Don't print status updates while reading files — do the reading, then present the candidates.
3. **Specific candidates only.** Every candidate names a real task from `domains.md`. Generic suggestions fail.
4. **Connection-check every candidate.** If a required tool isn't in `connections.md`, label it `Needs [tool] first`.
5. **Never re-suggest what's been built or scoped.** Check skills and decisions log before generating candidates.
6. **Deep dive is optional.** Don't force it. Some clients pick a candidate on instinct and want to go straight to `/level-up`.
7. **Three to five candidates.** Not two (not a real choice), not six (decision fatigue).
8. **Write to `runs/` every time.** Even if no deep dive was done. This feeds the ROI report.
9. **Read-only on all files except `decisions/log.md` and `runs/`.** Don't modify context, skills, or connections.

## Verification (for the implementer)

- **Cold run.** No prior decisions in log, no prior skills built. Expected: 3-5 candidates pulled directly from domains.md tasks. Generic output ("you should automate your email") = fail. Every candidate must name a specific task.
- **Connection-check test.** Wire only one Tier-1 domain. Expected: candidates for the wired domain labeled "Buildable now", candidates needing other tools labeled "Needs [tool] first."
- **No-duplicates test.** Pre-populate decisions/log.md with a scoped automation. Expected: that automation does not appear as a candidate.
- **Deep dive gate.** Client can't answer Blueprint Process questions. Expected: skill stops and tells them to think it through first before returning.
- **Handoff test.** Client says "this one's clear, let's build it." Expected: skill closes with the one-screen summary and directs them to `/level-up` with the specific candidate name.
