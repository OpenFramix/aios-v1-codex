# Business Scorecard Rule

A passive, always-on rule. Loaded every session. Maintains a living model of what's healthy, what's stalling, and what's been quietly ignored in this business. Files it when it's worth acting on. Silent the rest of the time.

This rule is how the AIOS notices things the client didn't think to mention — and surfaces them at exactly the right moment.

---

## What to watch for

**Untracked metrics:**
The client mentions a number they care about — conversion rate, response time, retention, whatever — that has no corresponding tracking mechanism in the business. If the North Star Metric from `context/about-me.md` isn't being measured anywhere visible, that's a gap worth surfacing.

**Stalled domains:**
Read `context/domains.md`. If a domain has been mentioned in sessions but has had no skill activity, no level-up spec, and no candidate in `context/candidates.md` for 30+ days — that domain is stalling. The business is still doing that work manually. That's the radar pinging.

**Decisions that haven't moved:**
Read `decisions/log.md`. If a decision was logged more than 30 days ago with no follow-up entry, no tracking file created, and no mention in recent sessions — it either fell through the cracks or got quietly abandoned. Both are worth naming.

**The North Star showing up in conversation:**
If the client mentions their North Star Metric (from `context/about-me.md`) — whether they say the number is up, down, or unknown — note it. If it's moving in the wrong direction and no active candidate in `context/candidates.md` is pointed at it, that's a signal.

**Repeated problems:**
If the same issue, friction point, or domain comes up in two or more separate sessions — it's not a one-off. It's a pattern. Name it as a pattern the next time it surfaces.

---

## What to do with what you find

**When the observation is actionable — an automation opportunity:**
Append to `context/candidates.md` using the standard format:

```
## [Candidate Name]
Domain: [from domains.md]
Signal: [what was observed — specific, not vague]
ROI hypothesis: [what metric it moves + estimated impact]
Requires: [tools needed — check against connections.md]
Status: Ready to build / Waiting on [tool name]
Priority: High / Medium / Low
Surfaced: [YYYY-MM-DD]
Surfaced by: business-scorecard
Built:
```

**When the observation is informational — a pattern worth noting but not yet a build candidate:**
Append to `decisions/log.md`:

```
## YYYY-MM-DD — Scorecard: [short description]

**Type:** Stalled domain / Untracked metric / Stale decision / Pattern

**What was observed:**
[One or two sentences. Specific enough to act on. Not vague.]

**Candidate action:**
[What this suggests — a skill to build, a connection to wire, a priority to revisit, a conversation to have]

**Source:** business-scorecard rule
```

---

## When to surface

**Never interrupt active work.** Wait for a natural pause — task complete, topic shift, question asked.

Surface with one line:
> *"Scorecard note: [short description] — filed to [candidates.md / decisions/log.md]."*

**Maximum 2 observations per session.** If you spotted 4 things, pick the 2 most actionable. Filing obvious observations wastes log space and trains the client to ignore them.

**An observation must be specific enough that a future `/level-up` or `/explore` session could act on it without asking a follow-up question.** If it's too vague to act on, don't file it.

---

## What NOT to file

- Things already in `context/candidates.md` or `decisions/log.md` — don't duplicate
- Vague observations: "the client seems busy" or "there's a lot going on" — not actionable
- One-off requests that won't recur
- Anything that's already being addressed by an active automation or open candidate
- The same type of observation twice in one session

---

## Rules

1. **Silent by default.** This rule runs in the background. The client should never feel watched or audited.
2. **Specific or don't file.** If you can't name the candidate action, skip it.
3. **Max 2 per session.** Signal over noise.
4. **Never duplicate.** Check both `context/candidates.md` and `decisions/log.md` before filing.
5. **Append only.** Never edit or remove existing log entries.
