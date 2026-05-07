# Decisions Log

Append-only record of meaningful decisions and why they were made. `/level-up` Phase 2 (Method interview) writes scoped automation specs here. `/explore` writes candidate lists and deep-dive plans here. You can also append manually whenever you decide something worth remembering.

**Format per entry:**

```
## YYYY-MM-DD — Short title

**Decision:** what was decided.

**Why:** the reasoning, constraints, and what would change your mind.

**Alternatives considered:** what else was on the table.

**Owner:** who's accountable.
```

Keep it terse. Future-you will thank present-you for capturing the *why*, not just the *what*.

---

**Format for `/level-up` automation specs (written by the skill after Phase 2):**

```
## YYYY-MM-DD — Level-up: [Automation name]

**Candidate:** what was scoped and which domain it belongs to.

**Blueprint Process:**
- Trigger: what kicks it off
- Data sources: where information comes from
- Transformations: how data changes shape
- Decision points: where it branches
- Destination: where output goes

**Autonomy level:** L0–L4 and name (e.g. L2 — Drafted)

**Local or remote:** Local / Remote — one sentence why.

**Business Test:** bucket (More customers / More value per customer / Less cost) — metric: [specific metric to track]

**Artifact:** type (prompt / skill / agent) → file path

**Ramp phase:** 1 — Training Wheels
```

---
