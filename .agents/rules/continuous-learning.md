# Continuous Learning Hook

A passive rule loaded every session. Watch for intelligence worth capturing while working alongside the client — things that should inform the next `/level-up` or `/explore` session. File it in real time. Don't interrupt active work to do it.

The AIOS gets smarter between sessions because of this rule — not because the client asked it to, but because it was paying attention.

---

## What to Watch For

**Manual task signals:**
- Client describes doing something themselves: *"I spent time on..."*, *"every week I have to..."*, *"I always manually..."*
- A task the client asks for help with that recurs — if they're asking the AIOS to help with the same thing again, that's a skill candidate
- Copy-paste behavior: client pastes the same template, message, or format more than once in a session

**Bottleneck signals:**
- Expressed frustration: *"this always takes forever"*, *"I hate doing this"*, *"this is such a pain"*
- A decision that had to wait because information wasn't available: *"I had to check [tool] manually to find out..."*
- Something the client expected the AIOS to know but didn't — a gap in context

**Skill improvement signals:**
- Client edits the output of an existing skill every time it runs — suggests the skill's prompt needs tuning
- Client asks the AIOS to do something a skill already does, but differently — suggests the skill's approach is off
- A skill runs but the client doesn't use the output — the skill may be solving the wrong problem

**New tool signals:**
- Client mentions a tool not in `connections.md` or `context/tech-stack.md`: *"I checked in [tool]..."*, *"I got an alert from [tool]..."*
- A tool mentioned in passing that could unlock a new connection

---

## How to Capture

When you spot something worth keeping, file it immediately — don't batch at end of session.

**If the observation is an automation opportunity (manual task signal or bottleneck signal):**

Append to BOTH `decisions/log.md` AND `context/candidates.md`.

`decisions/log.md` entry:
```
## YYYY-MM-DD — Learning: [short description]

**Type:** Manual task / Bottleneck / Skill gap / New tool

**What was observed:**
[One or two sentences — specific enough to act on. "Client mentioned manually updating CRM after every call" not "client does manual work."]

**Candidate action:**
[What this suggests: a new skill to build, a connection to wire, an existing skill to improve, a context file to update]

**Source:** session observation
```

`context/candidates.md` entry (using standard pipeline format):
```
## [Candidate Name]
Domain: [from domains.md]
Signal: [what was observed — specific, matches the "What was observed" above]
ROI hypothesis: [what metric it moves + estimated impact]
Requires: [tools needed — cross-check against connections.md]
Status: Ready to build / Waiting on [tool name]
Priority: High / Medium / Low
Surfaced: YYYY-MM-DD
Surfaced by: continuous-learning
Built:
```

**If the observation is informational (skill gap, new tool signal, pattern — not a buildable automation):**

Append to `decisions/log.md` only. Do not add to `context/candidates.md`. The pipeline is for actionable build candidates, not general observations.

Keep entries terse. Actionable in under 30 seconds of reading.

When `/level-up` or `/explore` acts on a learning entry, append one line to that entry:
`**Acted on:** YYYY-MM-DD — [skill built / candidate scoped / connection added]`

This preserves the append-only rule while making addressed entries filterable. `/explore` and `/level-up` skip any learning entry that contains an "Acted on:" line.

---

## When to Surface

**Never interrupt active work.** Wait for a natural pause — task completion, a question asked, a topic shift.

Surface with one line only:
> *"Captured: [short description] → decisions/log.md + candidates.md"* (if automation opportunity)
> *"Captured: [short description] → decisions/log.md"* (if informational only)

**Max 2–3 captures per session.** Quality over quantity. If you spotted 5 things, pick the 2 most actionable. Filing obvious or generic observations ("client does some manual work") wastes log space and trains the client to ignore the captures.

A capture must be specific enough that a future `/level-up` or `/explore` session could act on it without asking a follow-up question. If it's vague, don't file it.

---

## How `/level-up` Uses This

When `/level-up` runs, after the stale automation check, scan `decisions/log.md` for learning entries filed since the last level-up session. If any exist, surface them before the Phase 1 interview questions:

> *"Before we start — I captured [N] thing(s) worth noting since last month:*
> *- [Learning entry summary]*
> *Want to start with one of these, or should I factor them into the candidate list?"*

If the client wants to start with a captured item — skip to Phase 2 (Method) directly with that candidate. The Mindset phase already happened in the background.

If the client wants them factored in — include them as weighted candidates during Phase 1. A captured observation from a real session outranks a hypothetical candidate surfaced from domains.md alone.

---

## What NOT to Capture

- Obvious recoverable things: a one-off bash command, a quick lookup, a formatting request
- Things already in `decisions/log.md` or already built as skills — don't re-file what's already known
- General complaints without a specific actionable signal: *"things are busy"* is not a capture
- The same type of observation twice in one session — once is enough

---

## Rules

1. **Silent by default.** Never interrupt active work. Surface only at natural pauses.
2. **Specific or don't file.** Vague captures are noise. If you can't name a candidate action, don't file it.
3. **Max 2–3 per session.** The log should accumulate signal, not noise.
4. **Never duplicate.** If an observation matches something already in the log or an existing skill — skip it.
5. **Append only.** Never edit or remove existing log entries. This is an append-only record.
