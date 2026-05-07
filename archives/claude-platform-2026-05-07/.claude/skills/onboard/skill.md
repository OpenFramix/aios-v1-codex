---
name: onboard
description: Use on Day 1 of an AIOS install, when someone says "set me up", "onboard me", "let's get started", or the intake form has just been filled. Combined wizard — processes the intake, researches the industry, generates the initial candidate pipeline, and scaffolds the full Day-1 file set. Idempotent — re-run any time after editing aios-intake.md.
---

## What this skill does

Single combined wizard. Reads `aios-intake.md`, conducts the interview if sections aren't filled, researches the client's industry, generates the initial automation candidate pipeline, then scaffolds all Day-1 files in one pass.

The output isn't just a set of files — it's a system that already knows what to build next.

**The wow moment:** at the end, show the client the top 3 automation candidates the AIOS has already identified for their business — with ROI hypotheses. Then ask: *"Which one do you want to build first?"* They should leave the first session feeling like the system already understands their business and knows exactly where the leverage is.

## When NOT to run this

- If the client has already onboarded and wants to refresh: still run, but the skill is idempotent — it backs up existing files and rewrites from current intake answers.
- If the operator wants to add a new connection mid-retainer: edit `connections.md` directly, then run `/audit` to update the score.

---

## Execution

### Step 0: Check for AI history export

Before anything else, check if `references/ai-history/` exists and has files.

- **Files present** → say: *"I found your AI history export. I'll process this and bake it into your context — this gives your AIOS institutional memory from day one."* Read the files, extract key business context (past decisions, recurring topics, stated goals, client names, product details). Synthesize — do not dump raw transcripts into context files.
- **No files** → say: *"No AI history found — no problem. If you have a ChatGPT or Claude export, drop it in `references/ai-history/` and re-run `/onboard` to absorb it. For now we'll build context from the intake."* Continue.

### Step 1: Read the intake

Read `aios-intake.md`. Check which sections have content vs. placeholder text.

- **All filled** → skip Step 2, jump to Step 1.5 (industry research).
- **Some filled** → say: *"I see [sections] are answered. Want to fill the rest now, or scaffold from what's there?"* Their call.
- **None filled** → run Step 2 conversationally.

### Step 2: The interview (9 questions)

Ask one at a time. Write each answer into `aios-intake.md` as you go so the session can resume if interrupted.

**Q1 — Who are you, what do you sell, and who do you sell it to?**
Identity, offer, ICP. Push for specificity — "small business owners" is not enough. Get the niche, the revenue range, the specific pain they're in, how money comes in.

**Q2 — Paste 1–2 things you've written recently. Don't edit them.**
*Hard rule — cannot be skipped or substituted.* Voice samples must be pasted raw, not typed mid-conversation. If they start typing fresh prose:

> *"Stop — paste it raw. Anything you write here is already shaped by our conversation. Open your sent folder or notes app and paste what's already there. This is the one rule I can't bend — your AIOS needs to sound like you, not like you trying to sound like yourself."*

Ask for two samples. An email, a text to a client, a social post — anything real.

**Q3 — Map your business like an org chart.**
Walk them through it verbally: "What are the main functions in your business? What actually happens every day?" Aim for 4–6 domains. Under each, capture 2–3 of the most common or most painful tasks. Push for specifics — "admin" is too vague, "manually typing every new client into a spreadsheet after they register" is what we need.

**Q4 — List every tool and software your business currently uses.**
Everything — even tools they barely use or are thinking about. Payments, email, scheduling, accounting, social, website, booking, CRM, files, communication. Also ask: *"What tools do you wish you had that you don't yet?"*

**Q5 — What are your 2–3 biggest priorities for the next 90 days?**
Quarterly priorities. Push back on vague goals — make them name a number, a deadline, or a deliverable. "Get more clients" → "Sign 5 new clients by August 1st."

**Q6 — What is your North Star Metric?**
*"If you had to pick one number that, if it moved in the right direction, would mean everything in your business is working — what is it?"* Could be enrollment rate, monthly revenue, student pass rate, retention rate, response time, anything. They name one. Current value and target if they know them.

**Q7 — What breaks first at scale?**
*"If 10x the clients showed up tomorrow, what's the first thing that would collapse? Not 'everything' — the specific first domino."*

**Q8 — What's your biggest untapped growth lever?**
*"What's the one thing that, if it ran on autopilot, would bring significantly more revenue or clients into your business? The thing you know you should be doing but can't get to?"*

**Q9 — What's eating your time, and what would prove this is worth it?**
Three parts: (1) biggest recurring time-suck, (2) the one specific output that would prove this was worth it in the first session, (3) where tasks and projects are currently tracked.

**Q10 — Brand & Delivery**

Before asking questions: *"Drop your logo files into the brand-assets/ folder right now — any format works. We'll extract colors from them and you won't have to describe your brand twice."*

Then walk through conversationally:

*"What's your website URL? I'm going to scrape it for colors and fonts so you don't have to name them from memory."* — write the URL to intake. If they don't have a website: *"Any site whose look and feel you like? Send me 1-2 URLs and I'll use those for style direction."*

*"What's your business name exactly as it appears on materials — and do you have a tagline?"*

*"I'll extract your brand colors from the site and logo. Do you happen to know your hex codes? If not, no problem — I'll pull them."* (capture hex if they know them — faster than scraping)

*"Same for fonts — do you know what fonts your brand uses, or should I pull them from the site?"*

*"How do you want your morning brief and monthly reports delivered — PDF, HTML, or Markdown? What time should the brief arrive, and what email?"*

Write all answers into `aios-intake.md` Q10 as you go. These answers plus the website scrape and logo analysis in Step 3.6 build the complete `references/DESIGN.md` — the one file every output-generating skill reads before producing anything client-facing. It follows the `@google/design.md` spec and is linted before the session closes.

### Step 1.5: Industry research

After the intake is complete (either filled or interviewed), research the client's industry before scaffolding.

Based on the business type from Q1, research and synthesize:
- **Common automation opportunities** in this type of business — what do operators in this space typically automate first?
- **Typical pain points** in this industry that the client may not have mentioned but almost certainly experiences
- **Market dynamics** — seasonality, compliance requirements, renewal cycles, exam cycles, certification windows, peak enrollment periods, anything industry-specific that the AIOS should know
- **Competitor landscape** — what are 2-3 comparable businesses in this space doing that this client isn't yet?

Synthesize into 3–5 industry observations. Do not show these to the client — use them to seed the candidate pipeline in Step 3.0. These are the things the system knows because it researched, not because the client told it.

### Step 3: Scaffold the Day-1 file set

Once intake and industry research are complete, generate all files. Back up any existing files to `archives/intake-{YYYY-MM-DD-HHMM}/` first.

**Step 3.0 — Generate the candidate pipeline first**

Before writing any other context files, run the analysis pass and write `context/candidates.md`.

Process:
1. Read all intake answers + industry research observations
2. For each domain task from Q3 marked repetitive, manual, or copy-paste → score automation potential (High / Medium / Low)
3. For each 90-day priority from Q5 → identify what automation would most directly accelerate it
4. For the North Star Metric from Q6 → identify what automation would most directly move it
5. For the scale-break from Q7 → identify the automation that would prevent it
6. For the growth lever from Q8 → identify the automation that would unlock it
7. Cross-reference against Q4 tool inventory — what's buildable with their current stack? What needs a connection first?
8. Add 2-3 candidates from industry research observations

Write `context/candidates.md`:

```markdown
# Automation Candidate Pipeline

Last updated: YYYY-MM-DD

---

## [Candidate Name]
Domain: [from domains.md]
Signal: [specific observation — what was seen that makes this a candidate]
ROI hypothesis: [what metric it moves + estimated impact — tie to North Star if possible]
Requires: [specific tools needed — from Q4 tool inventory]
Status: Ready to build / Waiting on [tool name]
Priority: High / Medium / Low
Surfaced: YYYY-MM-DD
Surfaced by: onboard
Built:

---
```

Target: 5–7 candidates. At least 2 should be `Status: Ready to build` based on tools already listed in Q4. At least 1 should connect directly to the North Star Metric.

**Step 3.1 — `context/about-me.md`**

From Q1 (identity, role) + Q9 (top time-suck). Two short paragraphs — who they are and what they're fighting against every week. Add a dedicated field:

```
north_star_metric: [from Q6]
north_star_current: [current value or "not tracking yet"]
north_star_target: [target value]
```

**Step 3.2 — `context/about-business.md`**

From Q1 (offer, ICP) + Q4 (tools) + Q7 (scale break) + Q8 (growth lever) + any relevant context from AI history. One paragraph on what the business does, one on who it serves, one on how money flows, one sentence on the scale break, one sentence on the untapped growth lever.

**Step 3.3 — `context/priorities.md`**

From Q5. Numbered list, one line per priority, with the specific number and deadline they named.

**Step 3.4 — `context/domains.md`**

From Q3 (org chart). The blueprint for the Capabilities layer.

Format:
```
# Business Domain Map

## Domain 1: [Name]
What happens here: [one sentence]
Daily tasks:
- [specific task]
- [specific task]
Automation potential: [High / Medium / Low]
Notes: [anything that came up in the interview about this domain]

## Domain 2: [Name]
...
```

This file is read every time a new skill is scoped. Specific task names matter — push back during the interview if answers are vague.

**Step 3.5 — `context/tech-stack.md`**

From Q4. Two sections:

```
# Tech Stack

## Tools in active use
[name — what it's used for — how critical — connected to AIOS: yes/no]

## Tools not yet connected to AIOS
[name — what it's used for — API/MCP available: yes/no/unknown]

## Tools the client wants but doesn't have
[from Q4 "wish list" — useful for future roadmap]

## Priority connections (wire first)
[top 2-3 tools based on Q5-Q9 answers and automation potential from domains.md]
```

**Step 3.6 — `references/DESIGN.md` — Active Brand Extraction**

This is not a form fill. It is an active extraction. Use every source available to build the most complete DESIGN.md possible before the session ends. Run the extraction in this order:

**A — Check brand-assets/ for logo files**
Read the `brand-assets/` folder. If logo files are present, note the filenames in the DESIGN.md `logo` section. Analyze the logo visually to extract the dominant brand colors as a starting point — primary, accent, and any neutrals visible in the mark.

**B — Scrape the client's website (if URL provided in Q10)**
Using WebFetch or the available web tools, fetch the client's website URL from Q10. Extract:
- Dominant background and foreground colors (from CSS or visual analysis)
- Heading and body font families (from `<link rel="stylesheet">` or `font-family` declarations)
- Any meta description or tagline
- General aesthetic: photography style, icon style, spacing density

If scraping is blocked or fails: note the URL in the Sources section and flag which fields need manual entry.

**C — Analyze reference sites (if provided in Q10)**
For each reference site listed, fetch and note the aesthetic direction. Do not copy their brand — extract the mood, spacing feel, and typography approach the client is drawn to.

**D — Fill remaining fields from Q10 interview answers**
Any field not resolved by extraction gets filled from Q10 answers. Hex codes the client stated directly, font names they named, delivery preferences.

**E — Synthesize into `references/DESIGN.md`**
Write the complete file. Populate every YAML frontmatter field. For any field that could not be determined, leave it as an empty string `""` and add a note in the Sources section flagging it for follow-up.

Color format: hex codes preferred for accessibility. OKLCH accepted if the client has a design system that uses it.

**F — Lint and validate**
After writing the file, run:
```
npx @google/design.md lint references/DESIGN.md
```
Fix any lint errors before closing the session. If the package is not available: validate manually that all required YAML frontmatter fields are present and no token references are broken.

**G — Surface gaps to Sam**
After lint passes, print a one-line summary:
> *"DESIGN.md built. [N] fields extracted from website, [N] from logo, [N] from interview. [N] fields still empty — flagged in Sources section for follow-up."*

The file is committed to the client's repo. Any missing fields get resolved at the Day 7 check-in if not during this session.

**Step 3.7 — `references/voice.md`**

From Q2. Paste samples verbatim. Header:

```
# Voice Reference

Match this register when drafting anything in this client's name.
Never generate external-facing content (emails, posts, proposals) without showing a draft first.

## Writing samples — verbatim

[Sample 1]

[Sample 2]

## Register notes
[One sentence characterizing the voice — tone, formality, word choice patterns. Written after reading the samples.]
```

**Step 3.8 — `connections.md`**

Populate the domain registry from Q4 answers and Q6–Q9 inferences. For each tool identified:

```
| # | Domain | Tool | Mechanism | Access | Auth | Last checked |
```

Set mechanism to `not yet connected` for all tools not yet wired. Flag priority connections from tech-stack.md with a note.

**Step 3.9 — Fill `CLAUDE.md` placeholders**

Fill all `{{...}}` placeholders using the scaffolded context files. Specifically:
- `{{Business Name}}` — from Q1
- `{{Owner Name}}` — from Q1
- `{{stated 90-day priority}}` — top priority from Q5
- Business context section — one-paragraph summary of what the business does and who it serves
- Domains section — list of domains from domains.md
- North Star Metric section — from Q6
- Voice section — one-sentence register summary from voice.md samples
- Connections section — tool list from connections.md (names only, not full table)
- Memory rule — include the vault-first rule and compact protocol verbatim:

```
## Memory Rule

Before answering any question about past decisions, previous work, client history,
or business context — read the relevant context files first. The files are the memory.
The chat is working space. When in doubt, check the file.

At 60% context, write a session summary to runs/session-summary-{YYYY-MM-DD}.md before
compacting. Include: decisions made, configurations set, and open action items.
Do not compact without writing first.
```

- Interface section — include placeholder:

```
## Interface

Phase 1 — Pending setup
Client access: [iMessage / Telegram — to be configured]
Phase 2 — Planned: Base44 dashboard (URL pending)

Note for operator: configure iMessage or Telegram channel after this session.
Update this section with the confirmed access method.
```

- `{{operator_name}}` — set from the `## Operator` section already in CLAUDE.md

### Step 4: Connection Sprint

After all context files are scaffolded and DESIGN.md is linted, run the Connection Sprint. This is done right now, during the setup session — not deferred to Day 2. Sam is at the computer. The client is present. Wire what can be wired today.

**Goal:** Leave the session with the AIOS reading real data from at least 2-3 of the client's actual tools.

#### Step 4.1 — Identify the sprint targets

Read `context/tech-stack.md` — Priority connections section. Read `connections.md` — current state. The sprint targets are the top 3 priority tools. Go in this order unless the client's stack says otherwise:

1. **Gmail** (communication + calendar + drive all share OAuth — one flow, four domains)
2. **GoHighLevel** (CRM + customer interactions + revenue — one API key, three domains)
3. **Notion / Slack / ClickUp** (knowledge / project tracking — based on Q4 answers)

#### Step 4.2 — Wire each connection

For each sprint target, walk Sam through the exact steps:

---

**Gmail (covers Domains: Communication, Calendar, Knowledge/files)**

*Via Cowork (recommended — no settings.json needed):*
- Cowork → Customize → Connectors → Google Workspace → Connect → OAuth flow → authorize
- Test: "List my 5 most recent emails." Confirm real emails appear.
- Then test Calendar: "What's on my calendar today?" Confirm real events.
- Then test Drive: "List my recent Google Drive files." Confirm real files.

*Via Claude Code (if delivering Code mode):*
- Copy `.claudecode/settings.json.example` to `.claude/settings.json`
- Add Gmail, Calendar, Drive MCP entries with client credentials
- Restart Claude Code → test same prompts above

---

**GoHighLevel (covers Domains: Revenue/Financials, Customer Interactions)**

- Log into GHL → Settings → Integrations → Private Integrations → Create New
- Scopes needed: Contacts (read/write), Opportunities (read/write), Calendars (read/write), Conversations (read/write)
- Copy the generated token
- Add to `.env`:
  ```
  GHL_PIT_TOKEN=paste_token_here
  GHL_LOCATION_ID=find_in_GHL_settings_under_Business_Info
  ```
- Test: "Fetch my 5 most recent GoHighLevel contacts." Confirm real contacts appear.
- Save `references/gohighlevel-api.md` if not already present (ships with the kit)

---

**Notion / Slack / ClickUp / Other (based on Q4 tech stack)**

For any tool in the priority connections list that has an MCP available:
- Cowork → Customize → Connectors → find the tool → Connect → OAuth or API key flow
- Test with a basic read query

For tools without an MCP (custom API):
- Create `references/{tool}-api.md` with the tool's base URL, auth method, and common endpoints
- Add the API key to `.env`
- Note the connection in connections.md as `key+ref` mechanism

---

#### Step 4.3 — Update connections.md

After each tool is wired, update the relevant row in `connections.md`:

```
| # | Domain | Tool | Mechanism | Auth | Last checked |
```

Set:
- `mechanism` = `mcp` (Cowork connector) or `key+ref` (API key + reference guide)
- `auth` = `connected`
- `last checked` = today's date

For tools that couldn't be wired today (credentials not available, tool not supported):
- Set mechanism = `not yet connected`
- Add a note in the row: reason + what's needed to wire it

#### Step 4.4 — Sprint summary

After working through all priority targets, print a one-line sprint result:

> *"Connection Sprint: [N] tools wired, [N] domains covered. [Tool names] are connected and returning real data. [Any remaining tools] still need [what's blocking them]."*

This goes into `decisions/log.md` as a dated entry.

**Time estimate:** 20-40 minutes for 3 connections. If it runs long, prioritize Gmail (highest leverage — unlocks brief delivery, email drafting, calendar awareness) and GHL (unlocks the most automation candidates).

---

### Step 5: The closing screen — Wow Moment

Print one screen. Make it land.

```
✓ Setup complete. Here's what I know about [Business Name].

You sell [offer] to [ICP].
Your North Star: [metric] — currently [value or "not yet tracked"].
Your biggest lever right now: [top candidate — one sentence].

──────────────────────────────────────

Top 3 highest-ROI moves I can see from here:

1. [Candidate name]
   [ROI hypothesis — one sentence]
   Status: Ready to build

2. [Candidate name]
   [ROI hypothesis — one sentence]
   Status: Needs [tool] first

3. [Candidate name]
   [ROI hypothesis — one sentence]
   Status: Needs [tool] first

──────────────────────────────────────

Ask me: "What should I focus on this week?"
Or pick one of the above and say: "Let's build it."

Next: wire your first connection — I recommend [highest-leverage tool from Q4].
Day 7: run /audit to score your AIOS and establish the baseline.

Installed by [{{operator_name}}].
```

When the client runs the closing prompt ("What should I focus on this week?"), respond using only the new context files:
- 3-bullet priority list in their voice register from Q2
- Each bullet tied to a stated 90-day priority from Q5
- Final line: *"If I had to pick one thing for this week, it's [X], because [specific reason from their priorities and North Star]. Want me to map out the first steps? And — the big question: what percentage of this could AI handle if we broke it down right?"*

---

## Critical implementation rules

1. **Voice paste cannot be skipped.** If they type samples mid-conversation, refuse and send them to their sent folder. The voice file is the one thing that can't be reconstructed later.
2. **Domain tasks must be specific.** "Admin" is not a domain. "Manually entering every new student into a spreadsheet" is a task. Push until you have real task names.
3. **Industry research before scaffold.** Don't skip Step 1.5. The candidate pipeline is only as good as the intelligence that went into it — and some of the best candidates come from what the system researched, not what the client mentioned.
4. **candidates.md is written first in Step 3.** Before any context file. It informs everything else.
5. **One-shot scaffold.** Write all Step 3 files in a single batch after the interview. No multi-turn confirmation during the scaffold.
6. **Idempotent.** Re-running backs up all existing context files to `archives/intake-{ts}/` first, then rewrites all files fresh from the current intake answers.
7. **Closing screen lands the wow moment.** The client should leave feeling like the system already knows their business. If the closing screen is generic, the onboarding failed.
8. **No extra skills generated on Day 1.** Skills are built during the retainer via `/explore` and `/level-up`.
9. **Connection Sprint happens on Day 1.** Wire at least 2-3 connections during the setup session. `.env` writes are expected and correct during the sprint. The goal is a connected AIOS before Sam walks out.
10. **AI history is synthesized, not dumped.** Extract business context from chat exports — don't paste raw transcripts into context files.
11. **Read-only on `references/ofx-blueprint.md`.** Framework reference ships with the kit. Don't overwrite.
12. **Brand variable.** The closing screen says "Installed by [{{operator_name}}]" — never hardcode a brand name.
13. **DESIGN.md is active extraction, not a form fill.** Always scrape the website first, analyze the logo second, fill from interview third. The goal is a complete file by end of session.
14. **Lint DESIGN.md before closing.** Run `npx @google/design.md lint references/DESIGN.md`. Fix errors before the closing screen.
15. **Step 4 is not optional.** The Connection Sprint is part of onboarding. An unconnected AIOS after setup is an incomplete install.

---

## Verification (for the implementer)

- **Cold-test:** Fresh install, run `/onboard`, fill all 9 answers, scaffold runs, ask the wow prompt. Response must cite their specific business from Q1, their North Star from Q6, their priorities from Q5, and their voice from Q2. Generic output = fail.
- **Candidate pipeline test:** After scaffold, `context/candidates.md` must have ≥5 entries. At least 2 `Status: Ready to build`. At least 1 connected to the North Star Metric. At least 1 sourced from industry research (not just intake answers).
- **Domain specificity test:** Give vague domain answers ("operations", "admin"). Expected: skill pushes back and asks for specific tasks before continuing.
- **Voice rejection test:** Type a fresh sample mid-interview. Expected: refusal and redirect to sent folder.
- **Industry research test:** Client is a certification school. Expected: candidate pipeline includes at least one candidate sourced from industry knowledge (e.g., student exam pass rate drop-off, course portal login rates) that the client didn't mention.
- **Idempotency test:** Re-run with one Q5 priority changed. Expected: backup created, files rewritten, candidates.md updated.
- **Brand variable test:** Change `{{operator_name}}` in CLAUDE.md. Expected: closing screen reflects the new name with no other changes needed.
