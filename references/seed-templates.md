# MiroFish Seed Templates

Use this file when you need stronger source material or clearer simulation requirements.

These templates are designed to improve:

- entity extraction quality
- stakeholder coverage
- persona richness
- simulation focus
- report usefulness

## Core Rule

Do not start with "predict X" alone.
Start with a compact world model:

- what happened
- who matters
- how they relate
- what evidence exists
- what uncertainty remains

## Source-Material Lint Checklist

Before uploading source material, confirm that it:

- names the main actors consistently;
- includes explicit dates or a clear time window;
- states at least a few concrete relationships;
- separates confirmed facts from open questions;
- avoids mixing multiple unrelated scenarios into one seed package;
- contains enough detail to distinguish actors from one another.

If you cannot check most of that list, improve the seed before touching runtime settings.

## Temporal Anchoring

MiroFish works better when the source package makes time explicit.

Include:

- the date of the trigger event;
- the sequence of major follow-up events;
- whether a fact is current, historical, or only proposed;
- what changed over time and what stayed stable.

Good pattern:

```text
On March 10, the regulator announced the draft rule.
On March 12, the company issued a response.
As of March 14, no formal enforcement action has happened.
```

Weak pattern:

```text
The regulator is watching the company and people are reacting.
```

## Naming Hygiene

Use one canonical name per actor across the whole source package.

Good:

- `Company Alpha`
- `Minister Chen`
- `Retail Investors`

Bad:

- `Alpha`
- `Alpha Inc.`
- `the company`
- `the platform`

If you build preprocessing or entity-normalization helpers outside MiroFish, prefer stable canonical labels and avoid near-duplicate entity names. When a stricter graph pipeline requires normalized labels, use PascalCase only in that preprocessing layer, not by turning the whole seed document into unnatural prose.

## Contradictions And Unknowns

Do not hide contradictions. Label them.

Useful pattern:

```text
Confirmed:
- The policy draft was published on March 10.

Disputed:
- Labor groups say the draft will cut wages.
- The ministry says wage impact is neutral.

Unknown:
- Whether the draft will pass without amendment.
```

## Template 1: Public Opinion Event

Use when the topic is a controversy, crisis, or fast-moving social narrative.

```text
Context:
Summarize the event, when it happened, where it happened, and why it matters.

Stakeholders:
- Organization or institution:
- Officials or spokespersons:
- Critics or opposition:
- Affected communities:
- Media and commentators:

Evidence:
- Timeline of key events
- Confirmed statements
- Public metrics, numbers, or trends
- Known open questions

Relationships:
Explain who influences whom, who is in conflict, and who is amplifying the issue.

Simulation requirement:
Analyze how public opinion may evolve over the next [timeframe].
Focus on narrative shifts, stakeholder reactions, media amplification, and trust changes.
```

## Template 2: Finance Or Market Scenario

Use when the topic is a price move, macro event, regulation, or market sentiment shift.

```text
Context:
State the asset, current conditions, recent price behavior, and key market backdrop.

Stakeholders:
- Regulators
- Exchanges or funds
- Analysts
- Institutional actors
- Retail sentiment groups

Evidence:
- Current price or valuation range
- Relevant macro indicators
- Regulatory actions
- Flow data, volume, or positioning
- Comparable historical moments

Relationships:
Explain how regulation, liquidity, technical indicators, and sentiment interact.

Simulation requirement:
Explore likely market narratives and directional scenarios over the next [timeframe].
Focus on regulation, flows, technical levels, and macro catalysts.
```

## Template 3: Product Launch Or Company Change

Use when the question is about adoption, reputation, competition, or partner response.

```text
Context:
Summarize the product, launch event, company change, or strategic move.

Stakeholders:
- Company leadership
- Customers
- Competitors
- Partners
- Media and analysts

Evidence:
- Launch details
- Pricing and positioning
- Public reactions
- Prior company performance
- Competitive benchmarks

Relationships:
Explain who benefits, who loses, who responds publicly, and who can shape adoption.

Simulation requirement:
Estimate how perception, adoption, and competitive response may evolve over the next [timeframe].
Focus on product-market fit, trust, differentiation, and ecosystem reaction.
```

## Template 4: Policy Or Regulation Scenario

Use when the key question is reaction to a draft law, policy shift, or enforcement change.

```text
Context:
Summarize the policy proposal or regulatory move and the decision timeline.

Stakeholders:
- Government bodies
- Regulated organizations
- Advocacy groups
- Experts
- Affected citizens or users

Evidence:
- Policy text or summary
- Official statements
- Historical precedents
- Economic or social impact estimates

Relationships:
Explain which actors support or oppose the proposal and what leverage they have.

Simulation requirement:
Project how stakeholder positions, public narratives, and implementation risks may evolve over the next [timeframe].
Focus on support, resistance, institutional friction, and downstream effects.
```

## Template 5: Fiction Or Storyworld Scenario

Use when MiroFish is being used for story extrapolation or character-world simulation.

```text
Context:
Summarize the world state, recent events, and the unresolved conflict.

Stakeholders:
- Main characters
- Factions or institutions
- Secondary actors with leverage

Evidence:
- Established motives
- Constraints and resources
- Known alliances and rivalries
- Key unresolved plot points

Relationships:
Explain trust, betrayal risk, dependence, and power asymmetry.

Simulation requirement:
Explore how the conflict may evolve over the next [timeframe or number of narrative beats].
Focus on alliances, strategy, emotional shifts, and likely turning points.
```

## Requirement Writing Pattern

Good simulation requirements usually specify:

- timeframe
- central question
- decision variables
- stakeholder reactions
- uncertainty boundaries

A stronger pattern is:

```text
Analyze how [scenario] may evolve over [timeframe].
Focus on [3-5 variables].
Watch for [coalitions, backlash, adoption shifts, liquidity stress, narrative drift].
Do not optimize for a single deterministic outcome.
```

## Requirement Add-Ons That Help

Add these only when they are genuinely relevant:

- geographic scope;
- platform emphasis (`Twitter`, `Reddit`, or both);
- specific stakeholder groups to watch;
- what would count as escalation, stabilization, or reversal;
- what evidence should matter most in the report.

## Anti-Patterns

- vague request with no timeframe
- single-perspective source material
- unnamed actors
- raw metrics without context
- large mixed-topic document for a narrow question
- no dates or temporal markers
- duplicate names for the same actor
- asking for certainty instead of scenario exploration
- adding confidential data just to make the seed more detailed
