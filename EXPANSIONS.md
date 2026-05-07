# EXPANSIONS — what to add as you grow

The kit ships lean on purpose. Six skills, five rules, core context folders, and one framework reference. As you use it, you'll outgrow the base — this guide tells you what to add, when, and why.

The AIOS structure should look like a small, well-run business. Not a hoarder's basement.

---

## What ships in the kit (don't remove)

| Folder / file | Purpose |
|---|---|
| `context/` | About you, your business, your priorities, your domain map, your tech stack. Filled by `/onboard`. |
| `references/` | Frameworks, voice samples, API guides, SOPs as you build them. |
| `references/ofx-blueprint.md` | The OFX Blueprint framework reference. Read-only — ships with the kit. |
| `decisions/log.md` | Append-only record of what was decided and why. Written by `/level-up`, `/explore`, and manually. |
| `connections.md` | Registry of every system your AIOS can reach. |
| `archives/` | Old files. Don't delete — move here. |
| `.agents/skills/` | Codex skills: `/onboard`, `/audit`, `/level-up`, `/explore`, `/morning-brief`, `/roi-report`. Add domain skills via `/level-up`. |
| `.agents/rules/` | Always-on operating rules for scorecard, change management, continuous learning, follow-through, and opportunity spotting. |
| `aios-intake.md` | Source-of-truth for `/onboard`. Edit and re-run any time. |
| `AGENTS.md` | Root operating manual. Filled by `/onboard`. Edit when your role or priorities change. |

**Auto-created by skills (not pre-built, but expected):**

| Folder / file | Created by | Purpose |
|---|---|---|
| `runs/` | All skills | Timestamped output files from every skill run. Required for ROI tracking. |
| `audits/` | `/audit` | Saved audit reports over time. Delta tracking shows the AIOS getting stronger each month. |

---

## What to add as you grow

| Folder / file | Add when | Why |
|---|---|---|
| `tracking/` | Auto-created by `/level-up` on first automation build | ROI tracking layer. Each automation gets a `tracking/{automation-name}.md` with frontmatter (`ramp-phase`, `domain`, `built`) and a time estimate. The `/roi-report` skill reads this folder to generate the monthly report. Do not manually create or delete this folder — `/level-up` manages it. |
| `projects/` | You're running 2+ ongoing workstreams with their own context | Active projects need scoped context separate from evergreen `context/` files |
| `templates/` | You catch yourself copy-pasting the same prompts or doc scaffolds | Reusable, parameterized starting points — reduces drift across skill runs |
| `brand-assets/` | You generate visual content (carousels, slides, thumbnails) | Centralizes logos, palettes, fonts, tone — the AIOS reaches in instead of guessing |
| `references/sops/` | You document how recurring processes run | Standard operating procedures the AIOS reads to run things consistently |
| `references/{tool}-api.md` | You connect a new API and figure out how it works | Researched-once-saved-forever. `/audit` scores this; future skills don't re-research. |
| `scripts/` | You write Python or Bash to hit APIs not covered by MCPs | Most second connections are scripts, not MCPs |
| `.agents/agents/` | You need a sub-agent spec for repeatable, multi-step research or writing | Agents run in their own context window — keep your main session lean |
| Sub-OS folders (e.g. `youtube-os/`) | You have a vertical with its own data, sheets, transcripts, scripts | Isolation pattern — vertical workflows get their own scoped operating manual and skills |

---

## Suggested cadences

When each surface gets routinely touched:

- `decisions/log.md` — every meaningful decision (`/level-up` Phase 2 and `/explore` deep dives write here automatically)
- `runs/` — auto-written by skills on every run; review monthly when generating the ROI report
- `audits/` — monthly after each `/audit` run; the delta line shows progress
- `tracking/` — updated by each automation run; the source data for the ROI report
- `archives/` — quarterly cleanup; move stale projects, deprecated skills, old intake versions
- `references/sops/` — when a process gets re-run by someone new, write the SOP
- `connections.md` — every time a new tool gets wired in, add a row
- `references/{tool}-api.md` — same time as `connections.md` update; capture the API once
- `AGENTS.md` — quarterly review; rewrite the priorities and business context sections when 90-day goals turn over

---

## What NOT to add

Anti-patterns. These look helpful but rot the structure:

- **Don't dump raw email or Slack archives into `references/`.** The wiki is not a doc dump. Interpreted facts only.
- **Don't build folder-of-folders for organization theater.** Flat with good naming beats deep nesting. If you need a folder hierarchy to find something, you have a search problem, not an organization problem.
- **Don't add `notes/`, `misc/`, `tmp/`, or `inbox/`.** Graveyards. Use `archives/` if it's old; write a real file in the right place if it's new.
- **Don't pre-create folders you don't need yet.** Empty folders are noise. The AIOS will tell you when it's time.
- **Don't have parallel `decisions.md` and `decisions/log.md`.** Pick one. The kit ships `decisions/log.md`.
- **Don't fork your operating manual.** One `AGENTS.md` at the root. Sub-OS folders can have their own scoped `AGENTS.md`, but the root is canonical.

---

## How to tell when it's time to add a folder

Ask three questions:

1. **Is this conceptually new?** Or does it fit somewhere existing?
2. **Will I touch this 3+ times in the next month?** If not, it's premature.
3. **Could `/level-up` route a future skill into here naturally?** If yes, the AIOS will use it. If no, you're organizing for yourself, not for the system.

Two yeses = add. One yes = wait.

---

---

## Operator Playbook

For operators installing and delivering this AIOS to clients.

### Install sequence (~2 hours with client)

**Before the session:**
1. Clone the repo to the client's VPS or local machine
2. Open in Codex — confirm all files are readable
3. Set `{{operator_name}}` in `AGENTS.md ## Operator` to your name/brand
4. Drop `VERSION.md` at root (copy from template, set install date)

**During the setup session:**
1. Ask client to export ChatGPT or Codex history → drop in `references/ai-history/` if available
2. Walk through `aios-intake.md` Q1–Q10 together — conversationally, not as a form
3. Run `/onboard` — reads intake, researches industry, scaffolds all Day-1 files, generates `context/candidates.md`
4. Run the wow moment: show the client their top 3 candidates. Ask: *"Which one do you want to build?"*
5. Wire Connection 1 (Gmail) — validate morning brief pulls real emails
6. Run `/audit` — establish baseline score; show client their starting point
7. Configure client access channel (Base44 dashboard URL, or messaging integration per deployment method)
8. Close: client knows what's next, the AIOS has already started

**Day 7:** Run `/audit` again. Wire Calendar. Review morning brief quality.
**Day 14:** Wire Drive. Run `/level-up` — build the first automation from candidates.md. Training Wheels.
**End of Month 1:** Wire n8n. Run `/roi-report`. Run `/explore` to refresh pipeline. Deliver report with invoice.

### Monthly retainer cadence

| When | Action |
|---|---|
| Start of month | `/explore` — refresh candidate pipeline |
| Mid-month | `/level-up` — build top candidate |
| Daily | Morning brief via client access channel |
| End of month | `/roi-report` — compile and deliver with invoice |
| Monthly | `/audit` — score delta, surface top gap |
| Quarterly | Update `AGENTS.md` priorities section as 90-day goals turn over |

### What to customize per client vs. what stays as OS defaults

**Customize per client:** `aios-intake.md` answers, `context/` files, `references/voice.md`, `connections.md`, `context/candidates.md` (generated fresh per client)

**Leave as OS defaults:** All skill files, all rule files, `AGENTS.md` behavioral sections (posture, voice, challenge instinct, etc.), `references/ofx-blueprint.md`

The OS is the product. The context is the customization. Never edit skill or rule files per client — upgrade the OS instead and all clients benefit.

### Common install failure modes

| Failure | Cause | Fix |
|---|---|---|
| Wow moment is generic | Voice samples were typed mid-session, not pasted raw | Re-run `/onboard` with pasted samples from sent folder |
| candidates.md is empty or thin | Industry research step was skipped | Re-run `/onboard` — the step runs automatically |
| Morning brief has no real data | Connections not wired | Wire Gmail and Calendar before running brief |
| Client does not use it after Day 1 | Access channel not configured | Configure the client access channel before closing the setup session |
| ROI report shows no time saved | `tracking/` files missing | Run the orphaned automation check in `/level-up` |

### Training a new operator

A new operator needs to know:
1. What the 5 layers are and why they're built in order
2. How to run the install sequence above, end-to-end
3. How the ramp phases work and why phase advancement is the operator's call only
4. How to read a `/audit` report and explain it to a client
5. How to run `/level-up` and deliver the artifact at the end

Practice install: run the full sequence on a concept business (like CareTech Academy) before installing for a real client. The practice install should produce a full `context/` set, a `candidates.md` with ≥5 entries, and a passing `/audit` score above 30.

---

## Phase 3 Access Roadmap

Phase 1 (iMessage/Telegram) and Phase 2 (Base44 dashboard) cover most clients through the first year. Phase 3 is for when you have 5+ active installs and need a scalable, white-labeled interface.

### When to build Phase 3

- 5+ active clients using the system daily
- Clients are asking for more features than Base44 can provide
- You want to white-label under your own brand with no visible Base44
- Mobile push notifications and voice input are worth the investment

### What Phase 3 requires that Phase 2 doesn't

- A backend API that reads from the AIOS file system (or a synced database)
- Authentication per client
- A proper deployment pipeline (not just sharing a Base44 URL)
- Custom notification logic for scheduled runs

### Technology options

| Option | Pros | Cons | When to choose |
|---|---|---|---|
| White-labeled Base44 | Fast, no backend needed | Limited customization ceiling | 5–10 clients, want speed |
| Next.js + Codex API | Full control, scalable | 2–4 weeks to build | 10+ clients, want full ownership |
| Custom mobile app | Push notifications, voice, native feel | 2–3 months, needs iOS/Android dev | 20+ clients, high-engagement use case |

Build Phase 3 only when Phase 2 is validated with real client usage. Phase 2 is fully capable through the first 12 months for most operator-client relationships.

---

> *Your AIOS structure should look like a small, well-run business — not a hoarder's basement. When you can't find something, that's a signal to consolidate, not to add another folder.*
