---
name: "roi-report"
description: "Use at the end of each retainer month to generate the client-facing ROI report. Reads runs/, tracking/, and audits/ to produce a one-page summary: automations run, time saved, AIOS health score, and what's queued next month. The report IS the retainer renewal argument — no call needed."
---

## What this skill does

Compiles everything the AIOS did this month into a one-page client-facing report. Not a technical log — a business case. The client reads it and understands, without needing a call, that the AIOS is delivering value and getting stronger over time.

**This report is the retainer renewal engine.** "Your AIOS ran 12 automations this month, saved approximately 6 hours, and your AIOS health score climbed from 54 to 71. Here's what's queued for next month." That is the renewal argument. No pitch needed.

## When `/roi-report` runs

- **Monthly — end of month.** Before sending the retainer invoice. The report accompanies the invoice as proof of value.
- **On-demand.** If the client asks "what has the AIOS actually done?" — run this.
- **Month 1 baseline.** The first run establishes the baseline. Every subsequent report shows movement vs. that baseline.

## Inputs the skill reads

- `runs/` — all timestamped output files from every skill run this period. File naming: `{skill}-{date}.md`. This is the activity log.
- `tracking/` — per-automation tracking files (`tracking/{automation-name}.md`). Each file holds the time estimate per run and business test metadata. Created by `/level-up` when an automation is built. If this folder is empty or missing, the time-saved section is estimated from runs/ filenames only — flag the gap.
- `audits/` — saved audit reports. The two most recent reports give the score delta for this period.
- `decisions/log.md` — level-up specs count as systems built; explore entries count as discovery sessions.
- `context/priorities.md` — connects this month's output back to the client's stated 90-day goals.

## Tracking file format (created by `/level-up`)

Each automation gets a `tracking/{automation-name}.md` when it's built:

```markdown
# Tracking: {Automation Name}

**Domain:** {domain from context/domains.md}
**Built:** {YYYY-MM-DD}
**Estimated time per run:** {X minutes — set at build time, updated as you learn actual time}
**Business Test bucket:** {More customers / More value per customer / Less cost}
**Metric:** {specific metric from the Business Test}
**Ramp phase:** {1 / 2 / 3 / 4 — update when you advance}

## Notes

{Anything worth capturing — edge cases found, improvements made, client feedback}
```

the operator sets the time estimate at build time based on how long the task took manually. Update it after a few runs if the actual time saved differs.

## Execution

### Step 1: Determine the reporting period

Default: the current calendar month. If run mid-month, use start of month to today. Confirm the period before reading files.

### Step 2: Read the activity log

Scan `runs/` for all files within the reporting period. Group by skill type:

- `level-up-{date}.md` files → automations built this month (count + names)
- `explore-{date}.md` files → discovery sessions this month
- `morning-brief-{date}.md` files already counted above
- `morning-brief-{date}.md` files → scheduled briefs delivered
- Any other `{automation-name}-{date}.md` files → automation runs (the automation is running on its own)

For each automation run file, note: which automation, what date, any output summary in the file.

### Step 3: Calculate time saved

Read `tracking/` folder. For each tracking file:
- Get the automation name
- Get the estimated time per run
- Count how many times that automation ran this month (from matching runs/ files)
- Calculate: runs × estimated time = time saved for that automation

Sum across all automations for total estimated hours saved this month.

**If `tracking/` is empty or missing:** Estimate based on runs/ activity only — count total automation runs and apply a conservative flat estimate (15 minutes per run as a floor). Flag this in the report: "Time estimates are approximate — add tracking files to improve accuracy."

**Cumulative:** Also calculate total runs and total estimated hours saved since install (all-time runs/ files × tracking estimates).

### Step 4: Read AIOS health score

Read the two most recent files in `audits/`. Extract:
- Previous audit score (layer-by-layer breakdown)
- Current audit score
- Delta: which layers improved, by how much

If only one audit exists → no delta yet. Note: "This is your baseline. Every report from here shows movement."

If no audits exist → flag as a gap. "Run `/audit` to establish your AIOS health baseline. This section will populate next month."

### Step 4.5: Read the pipeline value

Read `context/candidates.md`. Count entries where `Built:` field is blank (not yet shipped).

For each unbuilt candidate, extract the ROI hypothesis field. Where a time estimate is present, use it; where it's narrative, convert conservatively (e.g., "eliminates 15 min/student" × estimated monthly volume).

Add to the report between the time-saved section and the health section:

```
## What's in the Pipeline

[N] automations identified and ready to build:
- [Candidate name] — [ROI hypothesis, one line]
- [Candidate name] — [ROI hypothesis, one line]
[list Status: Ready to build candidates first, then Waiting On]

Potential additional capacity when built: ~[X] hrs/month

```

If `context/candidates.md` doesn't exist or is empty, omit this section entirely — don't flag it as a gap in the client-facing report. It's an operator gap, not a client concern.

### Step 5: Read what's queued

Scan `decisions/log.md` for the most recent explore entry. Extract the "Recommended next action" line. This becomes the "What's next" section of the report.

If no explore entry exists in the last 30 days → note: "Run `/explore` before next month to queue the next automation."

### Step 6: Compile and write the report

**Report format — client-facing, one page:**

```
# [Business Name] — AIOS Monthly Report
{Month YYYY}  |  Prepared by OpenFramix

---

## This Month at a Glance

Automations run:       {N} runs across {N} active systems
Estimated time saved:  ~{X} hours ({X} mins/run average)
Systems built to date: {N} ({N} added this month)
AIOS health score:     {N}/100 {▲+N vs. last month / — baseline}

---

## What Your AIOS Did This Month

{For each automation that ran, one line:}
- {Automation name} ({domain}) — ran {N} times, saved ~{X} min/run

{If explore sessions happened:}
Discovery sessions: {N} — surfaced {N} candidates for next month

{If level-up sessions happened:}
Built this month: {automation name(s)}

---

## AIOS Health

Score: {N}/100 — {Stage name}

{If delta exists:}
vs. last month ({date}):
  Context      {+N / 0 / -N}
  Connections  {+N / 0 / -N}
  Capabilities {+N / 0 / -N}
  Cadence      {+N / 0 / -N}
  Access       {+N / 0 / -N}
  Total        {▲+N}

{Top gap from most recent audit — one line with the recommended next step}

---

## What's Next

{From most recent explore entry or decisions/log.md:}
Queued for next month: {automation name} ({domain}) — {one-line why}

---

## Cumulative (Since Install)

Total systems built:   {N}
Total automation runs: {N}
Total est. hours saved: ~{X} hours

---

*Your AI Operating System — managed by {{operator_name}}.*
*Questions? Reply to this report or reach out directly.*
```

### Step 7: Save and prepare for delivery

1. Write the report to `runs/roi-report-{YYYY-MM}.md` — this is the only saved location. Do NOT write to `audits/` — that folder is for audit reports only and /audit reads it for delta calculations.
2. Ask: "Ready to send? I can draft an email to accompany this report."

If the client has a connected email (Gmail MCP or script), offer to draft the delivery email in their voice. Do NOT send without explicit confirmation.

**Delivery email draft (if requested):**
- Subject: `{Business Name} AIOS — {Month} Report`
- Body: 3-4 sentences summarizing the key numbers, mention what's queued for next month, close with "report attached"
- Tone: match `references/voice.md`
- Always a draft — never send automatically

## Output contract

Every `/roi-report` run produces:

1. **The report printed in chat** — full one-page report in the format above
2. **`runs/roi-report-{YYYY-MM}.md`** — saved report file
3. **Optional delivery email draft** — if client has email connected and confirms

## Critical implementation rules

1. **Client-facing language only.** No skill names, no file paths, no technical jargon in the report body. "Your AIOS ran 12 automations" — not "there were 12 entries in runs/."
2. **Honest estimates.** Never inflate time-saved numbers. If tracking data is sparse, use the conservative floor (15 min/run) and say so. Better to understate and overdeliver.
3. **Graceful degradation.** If `tracking/` is empty, still produce a report — flag the gap, use the conservative estimate. A partial report is better than no report.
4. **Month 1 is the baseline.** No delta line on the first report. The first score IS the baseline — all future movement is measured from it.
5. **Never send email automatically.** Always draft and confirm. This is an L2 — Drafted automation, not L4.
6. **Write to `runs/` every time.** Even a partial report gets saved.
7. **Read-only on all source files.** Never modify runs/, tracking/, audits/, or decisions/log.md while reading them.
8. **One report per month.** If a report already exists for this month in `runs/`, ask before overwriting: "A report for {month} already exists. Update it or keep both?"

## Verification (for the implementer)

- **Full data test.** Populate tracking/, runs/, and audits/ with sample data. Expected: report shows accurate run counts, time estimates, and audit delta. Numbers should be traceable back to source files.
- **Empty tracking/ test.** Remove tracking/ folder. Expected: report still generates, uses 15-min conservative estimate, flags the gap with instructions on how to fix it.
- **No delta test.** Only one audit file exists. Expected: report shows current score with "This is your baseline" — no delta line, no error.
- **Client language test.** Report must contain zero file paths, zero skill names (as technical references), zero markdown code blocks in the client-facing section.
- **Month 1 baseline test.** First ever run. Expected: all cumulative counts show actuals, no comparison to previous month, score labeled as "baseline."

## Dependency note

For the time-saved calculation to work, every automation built via `/level-up` needs a corresponding `tracking/{automation-name}.md` file. The `/level-up` skill should create this file as part of its output contract — see the level-up skill's Phase 3 section. If tracking files are missing for existing automations, the operator can create them manually using the format defined above.
