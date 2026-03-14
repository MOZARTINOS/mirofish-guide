# MiroFish Experiment Protocol

Use this file when you want MiroFish runs to be comparable, reproducible, and worth learning from.

## Purpose

MiroFish is stochastic. A single run can be suggestive, but it is not a dependable basis for guidance.

This protocol helps operators:

- compare conditions instead of anecdotes
- keep run logs reproducible
- reduce wasted budget
- extract signal from repeated runs

## Minimal Sufficient Protocol

Every experiment should specify:

1. The exact question being tested
2. The seed document or a stable identifier for it
3. The exact simulation requirement text
4. The variable being changed between conditions
5. The model or proxy route
6. The round count and effective scope
7. At least 3 runs per condition

## Core Experiment Pattern

### Step 1: Define a baseline

Run a stable baseline with no major intervention.

Example:

- same seed
- same requirement
- same model
- same round count

### Step 2: Change one variable

Only one major variable should change at a time.

Good variables to test:

- seed quality
- simulation requirement wording
- round count
- model family
- proxy route

### Step 3: Replicate

Run each condition at least 3 times.
If results vary wildly, increase replication before drawing conclusions.

### Step 4: Score

Use [evaluation-rubric.md](evaluation-rubric.md) after each run.

### Step 5: Compare

Compare both:

- mean quality across runs
- variance across runs

High average with huge variance is not the same as stable quality.

## Experiment Record Template

```yaml
experiment:
  name: ""
  date: "YYYY-MM-DD"
  purpose: ""
  hypothesis: ""

seed:
  id: ""
  word_count: 0
  notes: ""

simulation_requirement:
  text: ""

environment:
  mirofish_commit: ""
  llm_model: ""
  llm_base_url: ""
  zep_enabled: true

parameters:
  agent_count: 0
  round_count: 0
  platforms:
    - twitter
    - reddit

conditions:
  baseline: ""
  variant: ""
  variable_tested: ""

replication:
  runs_per_condition: 3

evaluation:
  simulation_total: 0
  report_total: 0
  combined_total: 0

artifacts:
  simulation_ids: []
  report_ids: []

notes:
  key_findings: ""
  failure_modes: ""
```

## Reproducibility Checklist

- [ ] Seed document preserved or hashed
- [ ] Simulation requirement preserved verbatim
- [ ] Model and proxy route recorded
- [ ] Agent count and round count recorded
- [ ] MiroFish version or commit recorded
- [ ] At least 3 runs per condition completed
- [ ] Evaluation scores logged for every run
- [ ] Major artifacts referenced

## Recommended Experiment Families

### Seed Quality Impact

Hold everything else constant.
Compare weak vs. structured vs. highly curated seed material.

Measure:

- entity relevance
- persona diversity
- report grounding

### Requirement Wording Sensitivity

Hold seed constant.
Compare vague vs. structured vs. scenario-specific simulation requirements.

Measure:

- interaction richness
- action diversity
- report specificity

### Round Count Sensitivity

Hold seed, requirement, and model constant.
Compare low, medium, and high round counts.

Measure:

- marginal quality gain
- cost growth
- variance across runs

### Model Or Proxy Comparison

Hold all inputs constant.
Compare one model or route against another.

Measure:

- setup reliability
- structured output stability
- report quality
- budget and latency

## Interpretation Rules

- Do not claim a general rule from one run.
- Do not mix multiple changed variables in the same comparison.
- Do not ignore failed runs; failure modes are data.
- When evidence is mixed, document that explicitly instead of forcing a conclusion.
