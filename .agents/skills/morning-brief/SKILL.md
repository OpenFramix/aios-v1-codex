---
name: "morning-brief"
description: "Use each morning to generate a daily brief — today's agenda, tasks due, overnight automation activity, and one focus recommendation. Designed to run on a schedule. Connection-aware — quality scales with what's wired. Readable in 60 seconds."
---

## What this skill does

Starts the day with context. What's on the calendar, what tasks are due, what the AIOS flagged or ran overnight, and one clear focus recommendation tied to the client's 90-day priorities.

Readable in 60 seconds. Not a report — a brief.

**Why it matters for the retainer:** The morning brief is the most visible daily proof that the AIOS is running. The client opens their dashboard or chat and sees their day already assembled. Over time, it becomes the thing they check before anything else — the AIOS is woven into how they start every day.

**This skill drives the Cadence layer score.** Running it through a Codex app automation is what earns the recurring trigger points in `/audit`. Without a recurring skill, the AIOS only runs when asked. With a scheduled morning brief, it runs on its own.

## When `/morning-brief` runs

- **Daily, first thing.** Designed to run on a schedule — 7–8am before the client's day starts.
- **On-demand.** Any time the client wants a day-start summary.
- **Start with Training Wheels.** Run it manually for the first two weeks. Confirm the output is useful. Then schedule it.

**How to schedule it** (once Training Wheels phase is validated):

Create a Codex app automation that runs `/morning-brief` at the client's preferred brief time from `references/DESIGN.md`. Weekends are optional. The automation must leave a dated output in `runs/` so `/audit` and `/roi-report` can verify cadence.

## Inputs the skill reads

Always available (no connection required):
- `context/priorities.md` — 90-day priorities. The focus recommendation always connects back here.
- `context/about-me.md` — role and top pain. Grounds the brief in what matters to this specific person.
- `decisions/log.md` — any recent decisions or scoped automations worth surfacing.
- `runs/` — any automation output files written since yesterday. If the AIOS ran something overnight, surface it.

Connection-dependent (brief degrades gracefully if not wired):
- **Calendar** (Google Cal MCP or equivalent) — today's scheduled events and meetings.
- **Task tracker** (ClickUp, Notion, Asana MCP or script) — tasks due today or overdue.
- **Communication** (Gmail MCP or equivalent) — flagged or high-priority emails from the last 18 hours.

## Execution

### Step 1: Check overnight automation activity

Scan `runs/` for any files written since yesterday at this time. If any exist:
- Note which automation ran and what it produced (read the summary line from the file)
- Surface it in the brief as "Overnight activity"
- If nothing ran → skip this section silently

### Step 2: Pull live data (connection-dependent)

**Calendar:** If wired, pull today's events. Note start time, title, and any back-to-back blocks.
If not wired → include a one-line placeholder: `"Calendar: not connected — wire Google Cal to see today's agenda here."`

**Tasks:** If wired, pull tasks due today and any overdue tasks (limit to top 5 to avoid noise).
If not wired → include: `"Tasks: not connected — wire your task tracker to see what's due today."`

**Email:** If wired, scan for emails marked urgent, starred, or unread from a known contact (use the client's CRM contacts as a filter if available). Limit to 2-3 flagged items max.
If not wired → skip this section entirely. Don't flag the gap here — email is optional in the brief.

### Step 3: Generate the focus recommendation

Read `context/priorities.md`. Identify which priority has the most momentum or most urgency based on:
- Any recent level-up or explore session in `decisions/log.md`
- Any overdue tasks pulled from the task tracker
- Proximity to the stated deadline from Q5

Pick one thing. One sentence. Tie it to a specific priority. Don't suggest multiple focuses — the point is clarity.

After the focus recommendation, check `context/candidates.md` for the top entry where `Status: Ready to build`. If one exists, add one line to the brief:

```
READY TO BUILD
[Candidate name] ([Domain]) — run /level-up when you have 30 min.
```

If no candidates are ready to build, omit this line entirely. Never show a "Waiting on connection" candidate in the morning brief — only show what's actually buildable today.

### Step 4: The Lens question

End every brief with The Lens applied to today's focus:

*"The Lens: what percentage of [today's focus task] could AI handle if you broke it down right?"*

This is not rhetorical. It seeds the OFX Blueprint's Mindset layer into the client's daily thinking. Over time they start asking it themselves before you do.

### Step 5: Compile and print the brief

**Format guidance — conversational when data is rich, structured when sparse:**

When calendar and task data is live and specific, write the brief like a GM speaking — not like filling in a form:
- "Your 10am runs into your 12pm — the enrollment follow-up needs to happen before then."
- "Three tasks are overdue. The registration backlog is the one that costs you money."
- "Nothing urgent in email — one thread from [name] worth a look before noon."

When data is sparse (connections not wired), fall back to the structured format with section headers.

**Brief format (structured fallback):**

```
Good morning. {Day, Date}.

AGENDA
{Calendar events with times — or "Calendar not connected."}

TASKS DUE TODAY
{Tasks due, max 5 — or "Task tracker not connected."}

OVERNIGHT
{What the AIOS ran or flagged since yesterday — omit if nothing ran.}

TODAY'S FOCUS
{One thing. One sentence. Tied to a priority.}

READY TO BUILD
{Top ready candidate from candidates.md — or omit if none ready.}

The Lens: what percentage of [{today's focus}] could AI handle if you broke it down right?
```

Keep it tight regardless of format. If a section is empty and the connection is missing, note it once and move on. Don't repeat gaps in multiple places.

### Step 6: Write to `runs/`

Save a copy to `runs/morning-brief-{YYYY-MM-DD}.md`. This feeds the activity count in the monthly ROI report. Each saved brief is evidence the AIOS is running.

## Ramp guide

| Phase | What happens |
|---|---|
| 1 — Training Wheels | the operator runs it manually each morning, reviews the output, confirms it's accurate |
| 2 — Guided | Scheduled to run automatically, the operator reviews before acting on any flagged items |
| 3 — Watched | Runs automatically, the operator glances at it each morning, spot-checks for accuracy weekly |
| 4 — Hands-Off | Fully autonomous — client reads it, acts on it, doesn't second-guess it |

Start at Phase 1. Advance only when the output has been accurate for 5+ consecutive runs at the current phase.

## Output contract

Every `/morning-brief` run produces:

1. **The brief printed in chat** — in the format above
2. **`runs/morning-brief-{YYYY-MM-DD}.md`** — saved for ROI tracking

## Critical implementation rules

1. **60 seconds, maximum.** If the brief takes longer than 60 seconds to read, it's too long. Cut ruthlessly.
2. **One focus only.** Never suggest two things to focus on. Clarity is the point.
3. **Graceful degradation always.** Missing connection = one line, move on. Never error out or refuse to produce a brief because data is missing.
4. **The Lens question is mandatory.** Every brief ends with it. No exceptions. It's how the OFX Blueprint gets installed into daily thinking.
5. **Overnight section is silent when empty.** Don't say "nothing ran overnight." Just omit the section. Only show it when there's something to show.
6. **Write to `runs/` every time.** Even a minimal brief (no connections wired) gets saved. Every file counts toward the ROI report activity total.
7. **Match the client's voice register.** Read `references/voice.md` before generating the focus recommendation. It should sound like how they talk to themselves, not like a formal assistant.
8. **Never send automatically without Phase 3+ validation.** If delivery is via email or Telegram, it must be Phase 3 before any automatic send. Phase 1 and 2 print in chat only.

## Verification (for the implementer)

- **No connections test.** No calendar, no tasks, no email wired. Expected: brief still generates with placeholder lines for calendar and tasks, focus recommendation from priorities.md, The Lens question. Never errors out.
- **Full connections test.** All three connections wired and active. Expected: real calendar events, real tasks due, email flags if any. Brief is still readable in under 60 seconds.
- **Overnight activity test.** Drop a sample runs/ file with yesterday's date. Expected: Overnight section appears with the automation name and what it produced.
- **One focus test.** Client has 3 priorities in priorities.md. Expected: brief recommends exactly one thing to focus on today, not all three.
- **The Lens test.** Expected: every brief ends with the question, applied to the specific focus recommendation — not generic.
- **Scheduling test.** Create the Codex app automation. Expected: brief runs automatically at the scheduled time and writes `runs/morning-brief-{YYYY-MM-DD}.md`.
