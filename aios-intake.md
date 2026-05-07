# AIOS Intake

This is the source-of-truth file for your AI Operating System. Fill this out before or during your setup session. The more specific your answers, the more powerful your AIOS will be from day one.

There are no wrong answers. Vague answers produce a generic system. Specific answers produce one that knows your business.

---

## Before You Begin — Export Your AI History

If you've been using ChatGPT or Codex, export your conversation history before the setup session. Your AIOS will use it to build context from day one — no re-explaining your business from scratch.

- **ChatGPT:** Settings → Data Controls → Export Data → download and unzip → find `conversations.json`
- **Codex:** export any relevant Codex thread summaries or project notes

Drop the files in `references/ai-history/` during the setup session. If you don't have an export yet, skip it — we can add it later.

---

## Q1 — Who are you, what do you sell, and who do you sell it to?

Your identity, your offer, and your ideal client. Push past the generic. "Small business owners" is not enough. "Med spa owners doing $300K–$1M who are losing leads after hours because their front desk leaves at 5pm" is what we need.

Include: your name and role, what the business is called, what you sell, who you sell it to (specific — revenue range, pain they're in, where they are in their journey), and how money comes in.

```
[Your answer here]
```

---

## Q2 — Paste 1–2 things you've written recently. Do not edit them.

An email to a client, a text, a social post, a voicemail script, a proposal — anything that sounds like you when you're not trying. Paste verbatim. Do not write fresh samples here.

Open your sent folder or notes app and paste what's already there. This is how your AIOS learns to sound like you, not like a polished version of you.

**Hard rule: cannot be skipped or substituted.** If you type fresh prose here, the voice calibration will be off.

```
[Sample 1 — paste raw]
```

```
[Sample 2 — paste raw]
```

---

## Q3 — Map your business like an org chart.

What are the 4–6 main functions in your business? Think about what actually happens every week — not what you wish happened.

Under each function, list 2–3 of the most common tasks. Be specific. "Admin" is not a function. "Manually entering every new student into a spreadsheet after they register" is a task. That specificity is what lets the AIOS spot what's worth automating.

```
Function 1: [Name]
  - Task: [specific task]
  - Task: [specific task]
  - Task: [specific task]

Function 2: [Name]
  - Task: [specific task]
  - Task: [specific task]
  - Task: [specific task]

Function 3: [Name]
  - Task: [specific task]
  - Task: [specific task]

Function 4: [Name]
  - Task: [specific task]
  - Task: [specific task]

[Add Functions 5–6 if applicable]
```

---

## Q4 — List every tool and software your business currently uses.

Everything — payments, email, scheduling, files, social media, website, booking, CRM, accounting, communication, spreadsheets. Even tools you barely use or are thinking about getting. Include the ones you wish you had.

We won't connect everything on day one. But knowing your full stack means the AIOS can plan ahead and surface automation opportunities as each tool gets wired.

```
Active tools:
- [Tool name] — [what it's used for]
- [Tool name] — [what it's used for]

Inactive / dormant:
- [Tool name] — [why inactive]

Wish list / wanted:
- [Tool name] — [why you want it]
```

---

## Q5 — What are your 2–3 biggest priorities for the next 90 days?

Not yearly goals — this quarter only. Things that, if they're not done in 90 days, you'd say you wasted the quarter.

Name a number, a deadline, or a specific deliverable. "Get more clients" is not a priority. "Sign 5 new clients by the end of July" is.

```
1. [Priority — with a number, deadline, or deliverable]
2. [Priority — with a number, deadline, or deliverable]
3. [Priority — with a number, deadline, or deliverable]
```

---

## Q6 — What is your North Star Metric?

If you had to pick one number that, if it moved in the right direction, would mean everything in your business is working — what is it?

Could be: monthly revenue, enrollment rate, client retention, response time, number of active clients, conversion rate — anything. Just name the one. Your AIOS will filter every recommendation through this number.

```
North Star Metric: [metric name]

Current value: [current number]

Target value: [target number and deadline]
```

---

## Q7 — What breaks first at scale?

If 10x the clients showed up tomorrow, what's the first thing that would collapse? Be specific — not "everything," but the actual first domino.

This is where the highest-leverage automation usually lives.

```
First domino: [specific process or function that breaks first]

Second break: [what fails next]

Notes: [any constraints or context worth capturing]
```

---

## Q8 — What's your biggest untapped growth lever?

What's the one thing that, if it ran on autopilot, would bring significantly more revenue or clients into your business? The thing you know you should be doing but can't get to because you're stuck in operations.

```
[Your answer here]
```

---

## Q9 — What's eating your time, and what would prove this is worth it?

Two parts:

1. The single biggest time-suck or task you dread every week. The thing that always takes longer than it should and never feels done.

2. The one problem that, if your AIOS handled it in the first session, would make you say "this is worth every penny." Be specific — what would it need to do, and what would it produce?

Also: where do you currently track tasks and projects? (ClickUp, Notion, Asana, a notebook, "I don't really track anything")

```
Biggest time-suck: [specific task or process]

First win that would prove it: [specific outcome — what it does and what it produces]

Where tasks live: [tool or method]
```

---

## Q10 — Brand & Delivery

**Before filling this section:** Drop your logo files into `brand-assets/` right now. Any format (PNG, SVG, JPG). The onboarding will extract colors from them — you won't have to describe your brand from memory.

---

**Website URL** (for color and font extraction):
```
[https://yourwebsite.com — or "no website yet"]
```

**Reference sites** (1-2 sites whose look and feel you like — used for aesthetic direction if no website):
```
[https://... — or "none"]
```

**Business name as it appears on branded materials:**
```
[Exactly how it reads on your logo, website, and documents]
```

**Tagline** (if you have one):
```
[Tagline or "none"]
```

**Brand colors** (hex codes if you know them — if not, leave blank and we'll extract from site/logo):
```
Primary:    [#hex or blank]
Secondary:  [#hex or blank]
Accent:     [#hex or blank]
Background: [#hex or blank]
Text:       [#hex or blank]
```

**Typography** (leave blank if unknown — we'll extract from site):
```
Heading font: [e.g. "Playfair Display" — or blank]
Body font:    [e.g. "Inter" — or blank]
Font source:  [Google Fonts / Adobe / custom / unknown]
```

**Visual style** (describe in plain English — used if site scrape is unavailable):
```
Overall aesthetic: [e.g. modern + clinical, warm + approachable, bold + energetic]
Photography:       [real photos / lifestyle / illustration / none yet]
Icons:             [flat / outlined / filled / don't use icons]
Spacing:           [airy / balanced / tight]
```

**Logo files in brand-assets/** (list filenames once dropped in):
```
[e.g. logo-dark.png, logo-light.svg, icon.png]
```

**Email & report delivery:**
```
Preferred format for reports and briefs: [PDF / HTML / Markdown]
Morning brief delivery time:             [e.g. 9:00 AM ET]
Deliver reports and briefs to email:     [email address]
Send from email:                         [email address — must be connected Gmail or configured sender]
```

---

When this file is filled, run `/onboard` and the wizard will scaffold your Day-1 setup: context files, voice reference, brand DNA, connections registry, domain map, initial automation candidate pipeline, and a filled operating manual. The setup session takes about two hours.

*Your AI Operating System. Installed by {{operator_name}}.*
