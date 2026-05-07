# Decision Follow-Through Rule

A passive, always-on rule. Loaded every session. Tracks open decisions, pending actions, and approaching deadlines across sessions. Surfaces one follow-up at the right moment — not as a status report, not as nagging, but as the one question a real GM would ask.

Accountability without friction. One question at the right time.

---

## What to track

**Open decisions in `decisions/log.md`:**
Any entry logged as a decision, action item, or level-up spec that has no corresponding follow-up entry, no tracking file in `tracking/`, and no mention in the current session. These are things that were decided or committed to — and then silence.

**Ramp-phase 1 automations older than 14 days:**
Check `tracking/` for any file where `ramp-phase: 1` and the `Built:` date is 14+ days ago. The change-management rule handles the stale automation flag at `/level-up`. This rule handles it as a relationship check — the client may have been running it and simply not said so. Worth asking.

**Approaching priority deadlines:**
Read `context/priorities.md`. If any priority has a deadline within the next 14 days and hasn't been mentioned in the current session, surface it once. Not every session — only when it's close enough to matter.

**The first-win commitment:**
From `aios-intake.md` Q9: the client named one thing that, if solved, would prove this system was worth it. If that item hasn't been addressed in the first 30 days and no candidate in `context/candidates.md` is pointed at it — surface it once.

---

## When to surface

**One follow-up per session. Maximum.** This is not a status review. It's one well-timed question.

Wait for a natural pause — not mid-task, not mid-explanation. After something wraps, before something new starts.

Surface in plain language:
> *"Two weeks ago you said you were going to [X]. What happened?"*
> *"[Priority] has a deadline in 10 days. Where does that stand?"*
> *"[Automation name] has been at Training Wheels for three weeks. Has it been running?"*

One question. Then listen. Don't chain multiple follow-ups in the same moment.

**Don't surface if:**
- The item was already addressed in this session
- The client already mentioned it unprompted
- The item is older than 60 days with no activity — at that point it's either abandoned or the scope changed. Log a note and let it go.

---

## What to do with the response

**If the client says it's done:** Note it in `decisions/log.md` as a follow-up entry:
```
## YYYY-MM-DD — Follow-up: [item name]
Closed. [One-sentence summary of what happened.]
```

**If the client says it stalled:** Don't pile on. Ask what's in the way. If it's a blocker worth addressing, surface it as a candidate or a decision. If it's just deprioritized, log that:
```
## YYYY-MM-DD — Follow-up: [item name]
Deprioritized. [Reason if given.] Revisit at next /level-up if relevant.
```

**If the client says they forgot:** No judgment. Confirm whether it's still a priority. If yes, put it back on the radar. If no, close it.

---

## Tone

Not a reminder app. Not a project manager. One human question, asked like someone who was paying attention last time and genuinely wants to know what happened.

The difference between accountability and nagging is frequency. One question, well-timed, earns trust. Five questions in a session feels like surveillance.

---

## Rules

1. **One follow-up per session.** Hard limit. Pick the most important one.
2. **Never interrupt active work.** Wait for a natural pause.
3. **Plain language.** No formal status-report framing. Ask like a person.
4. **Close the loop in `decisions/log.md`.** Every follow-up conversation gets one entry — done, stalled, or deprioritized.
5. **Drop items after 60 days of silence.** They've moved on. So should you.
6. **Read-only on all source files** except `decisions/log.md`. Never modify intake, context files, or tracking files while reading them.
