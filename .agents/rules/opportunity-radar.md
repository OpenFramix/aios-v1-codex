# Opportunity Radar Rule

A passive, always-on rule. Loaded every session. Scans what the AIOS already knows about the business and surfaces automation opportunities the client hasn't noticed or mentioned. Appends them to `context/candidates.md` when they're specific and actionable.

This is proactive intelligence — the AIOS noticing things on its own, not waiting to be asked.

---

## What to scan for

**Domains with no pipeline coverage:**
Read `context/domains.md`. For any domain marked with high automation potential that has zero entries in `context/candidates.md` and no built automation in `tracking/` — that domain is unserved. If the right connection is now wired (check `connections.md`), a candidate is ready to be written.

**Newly-unblocked candidates:**
Read `context/candidates.md`. For any entry with `Status: Waiting on [tool name]` — check `connections.md`. If that tool is now connected, update the entry to `Status: Ready to build` and surface it. A newly-wired connection often unlocks multiple candidates at once.

**New tool signals in conversation:**
If the client mentions a tool that isn't in `connections.md` or `context/tech-stack.md` — *"I checked in [tool]…"*, *"I got an alert from [tool]…"*, *"we just started using [tool]"* — that's a new tool signal. Note it. If it's a tool that could unlock automation, surface it as a connection worth wiring.

**Seasonal and cyclical patterns:**
Based on the client's industry (from `context/about-business.md`) and the current date — are there patterns that should be on the radar right now? A certification school in January has enrollment season coming. A retail business in October is approaching their highest-volume month. If a seasonal pattern is approaching and no automation is in place to handle it — that's a candidate.

**The growth lever from intake:**
From `aios-intake.md` Q8 (Growth lever) and the candidate pipeline — if the growth lever the client named has no active candidate pointed at it after 30 days, surface it. It was the thing they said would move the needle. If it's still manual, that's a gap worth naming.

**The scale-break from intake:**
From `aios-intake.md` Q7 (Scale break) — the thing that would break first at 10x volume. If there's no automation or candidate addressing it after 30 days, it deserves a place in the pipeline.

---

## How to write a candidate

When you identify a genuine opportunity, append to `context/candidates.md`:

```
## [Specific candidate name — not a category, a specific task]
Domain: [from domains.md]
Signal: [what was observed — specific enough to act on without follow-up questions]
ROI hypothesis: [what metric it moves + estimated impact — tied to North Star if possible]
Requires: [specific tools — cross-check against connections.md]
Status: Ready to build / Waiting on [tool name]
Priority: High / Medium / Low
Surfaced: [YYYY-MM-DD]
Surfaced by: opportunity-radar
Built:
```

**Hard rule on specificity:** "Automate follow-ups" is not a candidate. "Send a follow-up email 24 hours after a student completes registration but hasn't logged into the course portal" is a candidate. If you can't write a specific signal and ROI hypothesis, don't file it.

---

## When to surface

**Never interrupt active work.** Wait for a natural pause.

Surface with one line:
> *"Captured: [one-line description] → candidates.md"*

**Maximum 1–2 new candidates per session.** Quality over volume. A pipeline of 20 vague candidates is useless. A pipeline of 7 specific, high-ROI candidates is what gets things built.

**Don't surface if:**
- The opportunity is already in `context/candidates.md`
- The opportunity is already built (in `tracking/`)
- The observation is too vague to write a specific candidate entry
- You've already surfaced 2 this session

---

## Newly-unblocked candidate protocol

When a new connection is wired, run this check at the start of the next session:

1. Read `context/candidates.md` for all entries with `Status: Waiting on [tool]`
2. Check `connections.md` — is that tool now connected?
3. If yes — update the candidate entry: `Status: Ready to build`
4. Surface at the start of the session (before other agenda items):
> *"New connection wired — [N] candidate(s) just became buildable: [names]. Want to take one to `/level-up`?"*

This is the moment a new connection pays its first dividend. Make it visible.

---

## Rules

1. **Specific or don't file.** Every candidate must have a named signal and an ROI hypothesis. Vague = don't write it.
2. **Never duplicate.** Check `context/candidates.md` before writing. If it's already there, don't add it again.
3. **Cross-check connections.md.** Never file a candidate as "Ready to build" if the required tool isn't actually wired.
4. **Max 2 per session.** Signal over noise. The pipeline should accumulate insight, not clutter.
5. **Silent by default.** One-line surface at a natural pause. Never interrupt.
6. **Append only to candidates.md.** Never edit or remove existing entries. Mark as Built when shipped — don't delete.
7. **Read-only on all files except `context/candidates.md`.** Never modify context files, intake, skills, or connections.
