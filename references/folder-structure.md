# AIOS Folder Structure

Canonical layout for this AIOS install. Maintained automatically by `/organize`.
Last organized: `{{updated by /organize}}`

---

## Root

```
/
├── AGENTS.md              # Root system manual — how the AIOS thinks and behaves
├── EXPANSIONS.md          # Skill expansion and unlock rules
├── INSTALL.md             # Setup and onboarding instructions
├── README.md              # Overview of this AIOS install
├── VERSION.md             # OS version and changelog
├── aios-intake.md         # Onboarding intake form (business details, goals, voice)
├── connections.md         # Active integrations — what tools are connected and how
├── .gitignore             # Files excluded from GitHub sync
└── .agents/               # Platform layer (skills, rules) — managed by OpenFramix
```

## Folders

### `.agents/` — Platform layer (Codex)
Managed by OpenFramix. Do not edit directly.
```
.agents/
├── skills/                # All skills (/onboard, /audit, /organize, /sync-up, etc.)
└── rules/                 # Passive rules (always-on behavior)
```

### `context/` — Business brain
The AIOS reads these before every response. Keep them current.
```
context/
├── about-business.md      # What the business does, North Star, revenue model
├── about-me.md            # Who the operator is, communication style, background
├── candidates.md          # Automation candidates ranked by impact
├── domains.md             # Business domains and the specific tasks within each
├── priorities.md          # Current focus areas and urgency stack
└── tech-stack.md          # Tools, software, and integrations in use
```

### `references/` — Reference docs
Supporting material the AIOS uses when generating outputs.
```
references/
├── DESIGN.md              # Brand design system (colors, fonts, logo, email template)
├── voice.md               # Brand voice (tone, writing samples, what to avoid)
├── ofx-blueprint.md       # OpenFramix architecture and delivery standards
├── folder-structure.md    # This file — canonical folder map
└── {tool}-api.md          # Tool-specific API and integration notes (added as needed)
```

### `brand-assets/` — Brand files
Logos, fonts, and brand guidelines. Binaries are gitignored (not pushed to GitHub).
```
brand-assets/
├── logos/
├── fonts/
└── guidelines/
```

### `decisions/` — Decision log
Every significant business or AIOS decision goes here.
```
decisions/
└── log.md                 # Running log — newest entries at top
```

### `runs/` — Skill output history
Timestamped files from skill runs. This is the ROI evidence trail.
```
runs/
├── morning-brief-YYYY-MM-DD.md
├── session-summary-YYYY-MM-DD.md
├── level-up-YYYY-MM-DD.md
├── roi-report-YYYY-MM-DD.md
└── explore-YYYY-MM-DD.md
```

### `audits/` — Audit reports
Periodic AIOS architecture audits.
```
audits/
└── audit-YYYY-MM-DD.md
```

### `tracking/` — Ongoing tracking docs
Pipeline trackers, lead lists, project trackers. Anything with ongoing state.
```
tracking/
└── (client-specific tracking files)
```

### `archives/` — Archived material
Anything that's no longer active but shouldn't be deleted.
```
archives/
└── (dated archive folders or files)
```

---

## What belongs where

| File type | Goes in |
|---|---|
| `morning-brief-*.md` | `runs/` |
| `session-summary-*.md` | `runs/` |
| `audit-*.md` | `audits/` |
| `roi-report-*.md` | `runs/` |
| `level-up-*.md` | `runs/` |
| `explore-*.md` | `runs/` |
| Logos, fonts, brand images | `brand-assets/` |
| API notes for a tool | `references/{tool}-api.md` |
| Business decisions | `decisions/log.md` |
| Old/inactive files | `archives/` |
| Ongoing trackers | `tracking/` |

---

## What never moves

These files live at root and should never be relocated:
- `AGENTS.md`, `EXPANSIONS.md`, `INSTALL.md`, `README.md`, `VERSION.md`
- `aios-intake.md`, `connections.md`, `.gitignore`
- `.agents/` folder and all contents

The AIOS depends on these being exactly where they are.
