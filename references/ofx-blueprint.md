# The OFX Blueprint — Mindset, Method, Machine

> *"The best automation is the one you barely notice. Start by eliminating what doesn't need to exist, then automate what's left with the least amount of AI possible."*

**Simple Wins.**

---

## Why this is in your kit

This framework is the operator brain you'll use every time you run `/level-up`. Three layers, each one builds on the last. Read it once, refer back as needed.

Here's what most people get wrong: they think AI automation is about tools. It's not. Tools change every six months. What doesn't change is how you THINK about automation, how you DECIDE what to automate, and how you BUILD and OPERATE it once it's running. That's what the OFX Blueprint gives you — a way of thinking that works regardless of platform, model, or hype cycle.

---

## Layer 1 — MINDSET (How to Think)

Before you touch a single tool, you need to rewire how you approach work. The way you think about tasks determines whether you spot automation opportunities or walk past them every day.

### The Lens

The core habit: before doing any task the old way, ask — to what extent could AI handle this?

It's never binary. The real question is always **"what percentage of this could AI do?"** Maybe 80%. Maybe 10%. You don't know until you ask. The Lens trains you to ask before you assume.

**Real example.** Updating tracking links across 300 YouTube descriptions. Old way: open each one manually. Hours of drudgery. New way: describe the problem to Codex, walk to the kitchen. By the time you're back — researched the API, wrote the script, laid out the plan. Review, run, done. Now you have a reusable system.

Once The Lens clicks, you physically cannot go back. Every manual task starts to itch.

**One thing to internalize:** AI is better than you think and improving faster than you think. If it couldn't do something six months ago, try again now. Seriously.

### Function Breakdown

Your role is a set of functions. Each breaks into dozens of tiny tasks. You don't automate your whole job — you automate one tiny piece. Then another. Then chain them.

"Automate client onboarding" sounds impossible. Break it down: intake form, CRM entry, welcome email, folder creation, kickoff scheduling. Each piece is its own automation. Build one, get it working, move on.

One small task at a time. Six months later, dozens automated. Compounding is real.

### Curiosity Rule

Never accept AI output without asking why. Ask for alternatives. Ask which one it thinks is best and why. Push back. Dig in.

This is the antidote to automations you don't understand. **If you build something and can't explain how it works, you've built a liability, not an asset.** When it breaks — and it will — you'll have no idea where to start.

Treat AI as a mentor, not a vending machine. The vending machine gives you output. The mentor gives you understanding.

### Expect the Dip

Productivity drops ~20% for the first week or two. New workflows, new habits. That's normal. Push through. Fail fast, learn faster. Get to your first 10 mistakes safely and quickly — that's where the real learning lives.

---

## Layer 2 — METHOD (How to Decide)

Mindset tells you how to think. Method tells you what to do with that thinking — turning "I should automate something" into "here's exactly what I'm building and why."

### The Bottleneck

Two power questions surface everything:

**Q1:** *"If 500 new clients showed up tomorrow, what would break first?"* — finds bottlenecks. Onboarding? Invoicing? Support response times?

**Q2:** *"What would bring 500 new clients if it ran on autopilot?"* — finds growth levers. Content you're not creating? Leads you're not following up on?

One finds what's broken. The other finds what could scale. Start with the constraint.

### Three Gates

Every process goes through three gates — in this order, every time:

**Gate 1 — Cut it.** *"What happens if we just stop doing this?"* You'd be surprised how many processes exist just because they always have. Reports nobody reads. Approval steps that add no value. **If nobody would notice it disappeared, eliminate it. Don't automate waste.**

**Gate 2 — Automate it.** Apply The Mix 60-30-10:
- ~60% fully automated (no human touch)
- ~30% AI-assisted (AI does it, human reviews)
- ~10% stays manual (too nuanced, too risky, or too rare)

Full automation is rarely the right goal. If someone promises 100% on anything meaningful, they're selling you something.

**Gate 3 — Hand it off.** If a process can't hit the Mix — too complex, too variable, too judgment-dependent — delegate to a person. Not everything should be automated.

Nothing stays as-is. Every process gets cut, automated, or handed off.

### Blueprint Process

Before you touch any tool, map the process on paper. Five elements:

- **Trigger** — what kicks it off (form submission, email, time of day, event)
- **Data Sources** — where information comes from (CRM, inbox, spreadsheet)
- **Transformations** — how data changes shape (reformatting, filtering, combining)
- **Decision Points** — where it branches (if qualified → X, if not → Y)
- **Destination** — where output goes (CRM, email, Slack, document)

**Rule:** *if you can't explain it to a person, you can't explain it to AI.* Skip this step and you'll build something that sort of works but breaks in unpredictable ways.

### Autonomy Ladder

Each automation gets an autonomy level. Default to the lowest level that solves the problem:

| Level | Name | What happens |
|---|---|---|
| L0 | Manual | No AI. Human does it. |
| L1 | Suggested | AI suggests, human decides every step. |
| L2 | Drafted | AI drafts, human reviews and edits. |
| L3 | Supervised | AI runs, human validates periodically. |
| L4 | Autonomous | AI handles end-to-end. |

Most people jump to L4. That's where things go wrong. **Workflows beat agents. If a decision doesn't have to be made by AI, don't let AI make it.** Push autonomy up only after you've proven the lower level works.

### The Business Test

If your automation doesn't move a number, why are you building it?

Three buckets — every business metric falls into one:
1. **More customers** — content, outreach, lead gen, follow-up
2. **More value per customer** — premium delivery, upsells, retention
3. **Less cost** — eliminate drudgery, reduce errors, boost productivity

Plus a specific metric tied to the automation: response time, conversion rate, error rate, time saved.

If you can't name a bucket and a metric, stop building. "Because it's cool" isn't a business case.

---

## Layer 3 — MACHINE (How to Build and Operate)

You have the thinking (Mindset) and the decisions (Method). Now you build and run it. Two halves: BUILD and OPERATE.

### BUILD

#### Block by Block

Smallest possible steps. One input, one output per block. Output of block 1 becomes input of block 2.

Start with **zero-AI steps first**. Get the deterministic pieces working — data fetching, formatting, routing. Then layer in AI where it's actually needed.

This makes the project manageable and lets you validate as you go. If block 3 produces garbage, you know exactly where to look. Modularity is freedom.

#### One Job Rule

Each AI step does one specialized job. One call for drafting. Another for classification. Another for reasoning. Keep them separate.

Don't build a generalist. Specialized steps are easier to debug, easier to swap, easier to improve. When one breaks, you know exactly which job failed.

#### Test Steps

Validate each step's output before connecting to the next. **Do not build the whole pipeline and test end-to-end.** That's how you end up with "it doesn't work and I have no idea why."

Build step 1. Run it. Confirm output. Build step 2. Run it with step 1's real output. Confirm. Chain. That's how working systems actually get built.

#### Ship and Improve

There's no finished version of an AI automation. Deterministic scripts can be done. AI steps are always evolving — new models, new capabilities, better prompts.

Ship the working version. Get real-usage feedback. Improve from there. **Perfectionism is the enemy of deployment.** The version that's running is always better than the version that's perfect on paper.

### OPERATE

#### The Ramp

Roll out in phases:

| Phase | Name | What happens |
|---|---|---|
| 1 | Training Wheels | Run manually, operator confirms every output |
| 2 | Guided | AI drafts, operator reviews before it goes anywhere |
| 3 | Watched | AI runs, operator spot-checks periodically |
| 4 | Hands-Off | Fully autonomous — earned, not assumed |

Even at high confidence, start at Phase 1. Watch it run. Confirm the output. Then advance. This is not a limitation — this is how reliable systems get built.

Use confidence thresholds as you progress: high → proceed, medium → review queue, low → escalate. Tighten or loosen as data accumulates.

#### New Hire Rule

Treat every automation like a new employee on day one:

- **Own identity** — its own accounts and credentials, never the owner's
- **Read-only by default** — view-only until write access is proven necessary
- **Never impersonates the owner** — always signs as "AI assistant," not as the person
- **Scoped permissions** — API keys with minimum required scope, nothing more
- **Full audit trail** — every run logged, every action visible

*"You wouldn't trust someone you just met with your business accounts."*

#### The Teardown

Monitor what's running. If an automation consistently breaks, produces low-quality output, or costs more to maintain than it saves — **dismantle it.**

Don't fall into the sunk cost trap. Three weeks building something is not a reason to keep running it if it doesn't work. **Good operators know when to build AND when to destroy.** The Teardown is just as important as the launch.

---

## Governing Principles

Three principles that sit above everything. When in doubt, return here:

1. **Simple Wins.** Predictable beats clever. Default to the simplest, most deterministic approach that gets the job done.
2. **Deterministic steps can be finished. AI steps are always evolving.** Set expectations accordingly — yours and your client's.
3. **Fail fast, learn faster.** Get to your first 10 mistakes safely and quickly. Real learning lives there.

---

## Branch Frameworks

The OFX Blueprint is the foundation. Specific topics go deeper in dedicated references. These grow in `references/` over time:

- **The Integration Ladder** — API, CLI, Browser Automation, Scraping: hierarchy of reliability
- **The Error Handling Playbook** — what to do when things break
- **The Model Selection Guide** — how to pick the right model for the right job
- **The Context Engineering Framework** — how to feed AI the right information at the right time
- **The Discovery Playbook** — how to run discovery with a client before building
- **The Security and Permissions Playbook** — access control, audit trails, risk management
