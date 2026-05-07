# Change Management Rule

Every automation in this AIOS has a `ramp-phase` in its frontmatter. This rule governs how phases work, who can advance them, and what to do at each phase. Read this before executing any automation skill or helping the client advance a workflow.

---

## The Ramp Phases

| Phase | Name | What it means |
|---|---|---|
| 1 | Training Wheels | Runs manually. The operator reviews every output before anything leaves the system. |
| 2 | Guided | Runs automatically and produces a draft. The operator reviews and approves before the output goes anywhere. |
| 3 | Watched | Runs automatically. Output goes live. The operator spot-checks periodically. |
| 4 | Hands-Off | Fully autonomous. Earned only after Phase 3 has been validated. |

---

## Checking the Phase Before Running

Before executing any automation skill, check the `ramp-phase` value in the artifact's frontmatter.

**Phase 1 — Training Wheels:**
Run the automation and print the output in chat. Then add:
> *"Phase 1 — Training Wheels. Review this output before it goes anywhere. When this has run correctly 5+ times over 2+ weeks, the operator can advance it to Phase 2 by editing `ramp-phase: 1` → `ramp-phase: 2` in the frontmatter."*

Never send, post, update, or act on the output externally at Phase 1. Print only.

**Phase 2 — Guided:**
Run the automation, produce the draft, and present it for review. Then add:
> *"Phase 2 — Guided. Approve this before it goes out."*

Do not send or act externally until explicit approval is given in the same session.

**Phase 3 — Watched:**
Run and act. No confirmation required. Log the run to `runs/`. If output looks wrong, flag it immediately and do not proceed.

**Phase 4 — Hands-Off:**
Run and act. Fully autonomous. Log the run to `runs/`.

---

## Who Can Advance a Phase

**The operator only.** Clients do not advance phases.

Advancement requires the operator to manually edit the `ramp-phase` value in the automation's frontmatter file. The AIOS does not advance phases automatically under any circumstance — not based on run count, not based on time, not based on client request.

If a client asks to advance a phase, respond:
> *"Phase advancement is the operator's call — it requires confirming the automation has run correctly at least 5 times over at least 2 weeks. I'll flag this for the operator at the next `/level-up` session."*

---

## Advancement Criteria (for the operator's reference)

Before advancing any automation from its current phase, both conditions must be met:

1. **5+ confirmed runs** at the current phase with no output issues
2. **2+ weeks** at the current phase minimum

"Confirmed" means the operator reviewed the output and did not flag a problem. A run that produced wrong output, sent something it shouldn't have, or required manual correction does not count.

If both conditions are met, the operator advances by editing the frontmatter directly:
```
ramp-phase: 1  →  ramp-phase: 2
```
Also update `tracking/{automation-name}.md` with the new phase and the advancement date.

---

## Stale Automation Check (for `/level-up`)

When `/level-up` runs, run two checks before Phase 1:

**Check 1 — Stale automations:**
Check all `tracking/` files for automations where:
- `ramp-phase` is still `1`, AND
- The `Built` date is 14+ days ago

If any exist, surface them before Phase 1:

> *"Before we find something new to build — [N] automation(s) have been at Training Wheels for 14+ days:*
> *- [Automation name] (built [date])*
> *Want to review advancement on any of these first?"*

If the operator says yes, walk through the advancement criteria for each one and confirm both conditions are met before recommending the edit. If the operator says no, log the check in the session and move on.

**Check 2 — Orphaned automations:**
Cross-reference `runs/` against `tracking/`. Look for files in `runs/` that are NOT named `morning-brief-*`, `explore-*`, `level-up-*`, `audit-*`, `roi-report-*`, or `session-summary-*`. Any remaining named file is an automation run file. Check if a corresponding `tracking/{name}.md` exists.

If orphaned runs exist (no tracking file), surface them alongside Check 1:

> *"Also — I found [N] automation(s) in your run history with no tracking file: [names]. These aren't counting toward your ROI report. Want me to create tracking files for them?"*

If yes — create `tracking/{name}.md` for each, using the standard format with conservative time estimate (15 min/run as default) and a note: *"Time estimate is conservative — update after confirming actual run time."*

This keeps the ROI report complete and prevents automations from running invisibly without accountability.

This keeps the AIOS from accumulating automations stuck at Phase 1 forever — which inflates the build count without contributing to real Cadence layer maturity.

---

## Why This Rule Exists

A broken automation that fires without the operator's review is the fastest way to lose a client's trust. Training Wheels are not a delay — they're how reliable systems get built. Every automation that reaches Phase 3 or 4 earned it. That's what the retainer is worth.

Never skip this rule, even if the client pushes for it. Especially if the client pushes for it.
