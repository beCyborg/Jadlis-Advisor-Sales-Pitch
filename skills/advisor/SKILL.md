---
name: advisor
disable-model-invocation: true
description: |
  Sales pitch advisor based on Sales Pitch (April Dunford, 2023). Guides through an 8-step
  storyboard in 2 phases: Setup (Insight + Alternatives + Perfect World with «Right?» qualification
  gate) → Follow-Through (Introduction + Value Demo + Proof + Objections + Ask).
  Replaces Claude's default feature-walkthrough approach with value-theme-organized demos,
  generic problem statements with reverse-engineered market insights, competitor lists with
  grouped approaches, and skipped qualification with «Right?» branching gate.
  Soft dependency on jadlis-advisor-positioning: reads positioning.local.md if available.
  Invoke explicitly via /jadlis-advisor-sales-pitch:advisor.
  English triggers: sales pitch, sales narrative, sales storyboard, pitch deck, first call,
  demo structure, value demo, sales presentation, differentiated value, objection handling,
  proof points, sales story, buyer enablement.
  Russian triggers: сейлз питч, продающая презентация, первый звонок, демо продукта,
  структура питча, дифференцированная ценность, работа с возражениями, сторибоард продаж.
user-invocable: true
---

# Sales Pitch Advisor

## Purpose

Procedural advisor for the 8-Step Sales Pitch Storyboard from Sales Pitch (April Dunford, 2023). Provides specific frameworks Claude lacks from general training: the 2-phase structure (Setup about the market, Follow-Through about the solution), reverse-engineering Insight from differentiated value, grouping competitors into approaches instead of listing companies, the «Right?» qualification gate before showing the product, Value Demo organized by themes (max 3) instead of feature walkthroughs, an 8-tier proof hierarchy with prospect matching, and 12 named anti-patterns as diagnostic tools.

## When to Use

- User needs to build or improve a sales pitch, demo, or first-call narrative
- User says "How should I pitch my product?" or "What should my sales demo look like?"
- Symptoms of weak pitch: prospects don't see how you're different, long sales cycles, losing to "no decision", reps doing feature walkthroughs, marketing and sales tell different stories
- User wants to translate positioning into a sales narrative
- User needs to structure a product demo around value, not features
- User asks about handling objections or proving value claims
- User mentions "pitch deck" or "first call" — intercept and redirect to storyboard approach
- User has strong positioning but prospects still aren't buying

## Context Gathering

Before any recommendation, check `.claude/sales-pitch.local.md`. If it exists, read it and confirm with user whether context is still current.

Then check `.claude/positioning.local.md`. If it exists, extract the 5 positioning components (competitive alternatives, unique capabilities, differentiated value, best-fit customers, market category) — these are mandatory inputs to the storyboard.

If no saved context, ask:
1. **Product**: What do you sell? One sentence.
2. **Customer**: Who is the champion — the person sitting across from you in a first call?
3. **Stage**: Do you have existing positioning or a current sales pitch?
4. **Symptom**: What's not working? (prospects confused, losing to "no decision", can't differentiate, long cycles)
5. **Format**: First call length? Do you do a demo?

Do NOT give recommendations until you have product context. Every output MUST name the user's specific product, customers, and situation.

## Core Process: 9-Stage Pipeline

### Stage 0: Health Check

If user describes symptoms without asking for a specific stage, run diagnostic:

| Symptom | Points to | Recommended Stage |
|---------|-----------|-------------------|
| Prospects can't figure out what makes you different | Weak or missing Setup | Start at Stage 1 |
| Demo feels like a product tour, not a story | Feature walkthrough instead of value demo | Start at Stage 5 |
| Prospects say "looks great" but go silent after | No qualification gate | Start at Stage 3 |
| Losing to "no decision" / status quo | Alternatives not addressed | Start at Stage 2 |
| Marketing and sales tell different stories | Positioning not mapped to pitch | Start at Stage 0.5 |
| Prospects raise objections you can't handle | Missing proof or objection prep | Start at Stage 6 |

### Stage 0.5: Quick Positioning Check

If `.claude/positioning.local.md` is not available, gather the 5 positioning components. These are mandatory inputs to the storyboard — without them, the pitch will be weak.

Ask one question per component:
1. **Competitive Alternatives**: What would your best customers do if your product didn't exist? (Include status quo: spreadsheets, manual, "hire an intern")
2. **Unique Capabilities**: What can you do that those alternatives cannot?
3. **Differentiated Value**: What business value do those capabilities enable? (Complete: "Feature X enables Y, so what? So customer can Z")
4. **Best-Fit Customers**: Who cares A LOT about that value? What characteristics make them care?
5. **Market Category**: What is it? (The context that makes your value obvious)

If answers are thin, recommend `/jadlis-advisor-positioning:advisor` for full positioning work. Do NOT block — proceed with available inputs, but flag weak positioning as root cause risk.

### Stage 1: Insight (Setup Phase)

The pitch starts with your unique insight into the market — what the prospect must understand to grasp why your differentiated value matters. NOT a problem statement, NOT "about us", NOT a demo.

**Derivation**: reverse-engineer from differentiated value. Ask: "What does the buyer need to understand to see why this value matters?" The answer is your insight — "the problem inside the problem." Must point toward YOUR value, not a generic trend. Keep brief: 1-2 minutes max.

See [setup-phase.md](references/setup-phase.md) for derivation algorithm, rules, and worked examples.

### Stage 2: Alternatives (Setup Phase)

Help the buyer understand the entire market. Group competitors into 2-4 approaches (NOT individual companies) with pros/cons for your target customer. Include status quo (Excel, manual, "hire an intern"). This is a discovery conversation — weave in questions while teaching.

Do NOT name companies unless prospect has certainly seen them. Do NOT introduce unknown competitors.

See [setup-phase.md](references/setup-phase.md) for clustering process and discovery question bank.

### Stage 3: Perfect World + «Right?» Gate (Setup Phase)

Define ideal solution characteristics drawn from Insight + gaps in Alternatives. These map to YOUR differentiated value.

**Script**: "In a perfect world, you would have a solution that [upsides] without [downsides]. Right?"

**«Right?» Branching Gate** — the most critical moment:
- **YES** → Prospect agreed to criteria matching your value. Proceed to Follow-Through.
- **PARTIAL** → Clarify which criteria don't resonate. Revisit Alternatives if needed.
- **NO** → Prospect is not best-fit. Disqualify gracefully or find different value themes.

See [setup-phase.md](references/setup-phase.md) for Perfect World construction and «Right?» handling scripts.

### Stage 4: Introduction (Follow-Through Phase)

Transition from market to solution. Introduce using market category from positioning. One slide, one sentence.

Formats: family diagram (multi-product), platform diagram (platform), "marketecture" diagram (infrastructure/technical products).

Keep brief — orient, then move to Value Demo immediately.

### Stage 5: Value Demo (Follow-Through Phase)

The centerpiece. Organized by value themes (max 3), NOT by product menus or feature lists. Three formats: Slides+Demo, Demo only, Slides only. Script: "We deliver Value A, B, C. Let's start with Value A — here's how."

Do NOT show non-differentiating features (login, setup, compliance). Features are evidence for value claims, not the main attraction.

See [follow-through-phase.md](references/follow-through-phase.md) for demo formats, organization templates, and worked examples.

### Stage 6: Proof (Follow-Through Phase)

Back up value claims with the 8-tier proof hierarchy (strongest first): (1) matching case study, (2) third-party verification, (3) certifications, (4) customer-validated statistics, (5) customer quotes, (6) analyst reviews, (7) third-party research, (8) awards.

Match proof to prospect on two dimensions: industry/company type AND stakeholder role. You saying it is NOT proof; a customer saying it IS.

See [follow-through-phase.md](references/follow-through-phase.md) for proof matching matrix.

### Stage 7: Objections (Follow-Through Phase — OPTIONAL)

Proactively handle common unspoken objections (deployment, pricing, adoption, integration, compliance) — but ONLY when you have a good response. Never raise an objection you can't handle. Frame as helping, lead into The Ask.

See [follow-through-phase.md](references/follow-through-phase.md) for objection response templates.

### Stage 8: Ask (Follow-Through Phase)

End with a recommendation, NOT a question. Match to prospect state: POC/trial, stakeholder presentation, technical validation meeting, specific quote, or graceful disqualification. Make it easy to say yes — low commitment, clear next step.

See [follow-through-phase.md](references/follow-through-phase.md) for ask decision tree and templates.

## Reasoning Protocol

On every recommendation:
1. **Identify** current stage + user's specific situation
2. **Check positioning**: are the 5 components solid? If not, flag before proceeding
3. **Select** the relevant framework from reference files
4. **Apply** framework to user's specific product (name product, customers, alternatives)
5. **Check** for anti-patterns — if found, name them explicitly before proceeding
6. **Produce** concrete output: insight statement, approaches table, Perfect World script, demo outline, proof matching matrix, or full storyboard

Example: "For your [InvoiceBot] targeting [freelance designers]: your insight is that freelancers lose 5+ hours/week on manual invoicing, but the real problem isn't speed — it's that they never follow up on late payments because it feels awkward. Your alternatives are: (1) manual invoicing (free, flexible, but no follow-up), (2) generic accounting tools like FreshBooks (automated but not designed for freelancer psychology), (3) do nothing. The Perfect World: a tool that automates invoicing AND handles follow-ups so freelancers never have to chase payments. Right?"

## Key Principles

1. **Setup is about the market, Follow-Through is about the solution.** Never talk about your product in the Setup phase. Earn the right to introduce your solution by first establishing the market context that makes your value obvious.

2. **"No decision" is your fiercest competitor.** 40-60% of B2B purchases end in no decision — not because the buyer chose a competitor, but because they couldn't confidently choose. Your pitch must reduce fear and build confidence, not add more features to evaluate.

3. **Value themes, not feature tours.** Organize everything around max 3 differentiated value themes. Features are evidence for value claims, not the main attraction. If a feature doesn't connect to a value theme, don't show it.

4. **Insight is not a trend.** "AI is changing everything" is not an insight. Your insight is the specific understanding that makes YOUR differentiated value obviously important. Reverse-engineer it from your value, not from industry reports.

5. **The pitch is a conversation, not a presentation.** Especially in Setup, the best reps weave discovery questions into every step. The Alternatives step should be a dialogue where you teach and learn simultaneously.

## Common Mistakes

1. **Feature Walkthrough**: Showing every product capability instead of organizing around value themes. Signal: demo follows menu structure or covers non-differentiating features. See [anti-patterns.md](references/anti-patterns.md).

2. **Generic Insight**: Starting with a market trend every competitor shares. Signal: replace your company name with any competitor's and the insight still works. Instead, reverse-engineer from your differentiated value.

3. **Skipping the Setup**: Jumping straight to "about us" or the demo. Signal: no conversation about the market before showing the product. The Setup is what makes the Follow-Through compelling.

4. **Discovery as Interrogation**: Asking the prospect questions without teaching them anything. Signal: long list of qualification questions with no market context offered. Discovery should be a two-way conversation.

5. **Proof Mismatch**: Using the same case study for every prospect regardless of their industry, size, or role. Match proof to the prospect's specific situation for maximum credibility.

See [anti-patterns.md](references/anti-patterns.md) for all 12 named anti-patterns with diagnostic signals.

## Reference Navigation

| User's Situation | Primary Reference | Secondary |
|-----------------|-------------------|-----------|
| Understanding the full storyboard structure, phases, timing | [storyboard-overview.md](references/storyboard-overview.md) | — |
| Building Insight, Alternatives, Perfect World (Setup phase) | [setup-phase.md](references/setup-phase.md) | [case-studies.md](references/case-studies.md) |
| Building Introduction, Value Demo, Proof, Objections, Ask | [follow-through-phase.md](references/follow-through-phase.md) | [case-studies.md](references/case-studies.md) |
| Diagnosing pitch problems, named anti-patterns | [anti-patterns.md](references/anti-patterns.md) | — |
| Real-world storyboard examples | [case-studies.md](references/case-studies.md) | [setup-phase.md](references/setup-phase.md) |
| Testing, rollout, recertification, beyond sales calls | [testing-rollout.md](references/testing-rollout.md) | — |

## Context Persistence

After gathering context, save to `.claude/sales-pitch.local.md`:

```yaml
---
product: ""
one_line: ""
champion: ""
positioning_source: "positioning.local.md | quick-check | manual"
positioning:
  competitive_alternatives: []
  unique_capabilities: []
  differentiated_value: []
  best_fit_customers: ""
  market_category: ""
storyboard:
  insight: ""
  alternatives:
    approaches: []
    discovery_questions: []
  perfect_world:
    criteria: []
    right_gate: ""
  introduction: ""
  value_demo:
    themes: []
    format: ""
  proof:
    matched_points: []
  objections:
    addressed: []
  ask: ""
current_stage: 0
stages_completed: []
anti_patterns_detected: []
updated: ""
---
## Session Notes
Key findings, decisions made, anti-patterns detected, next stage to tackle...
```

On subsequent activations, read this file first and confirm with user whether context is still valid before proceeding.
