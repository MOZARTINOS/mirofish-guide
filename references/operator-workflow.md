# MiroFish Operator Workflow

Use this file when you need the practical loop for operating MiroFish end to end, not just a stage description.

For stage internals, also read:

- `references/workflow.md`
- `references/debugging.md`
- `references/evaluation-rubric.md`
- `references/experiment-protocol.md`

## The Short Version

1. define one scenario and one question;
2. build a clean source package;
3. run a small pilot first;
4. inspect artifacts before scaling;
5. scale only after the pilot looks real;
6. audit the report against raw evidence;
7. record the run in a reproducible format.

## Step 1: Define The Run

Write down:

- the scenario;
- the timeframe;
- the main variables to watch;
- what would count as a useful answer.

If the question is vague, MiroFish will produce vague configs and shallow reports.

## Step 2: Build The Source Package

Before upload, check:

- one focused scenario, not a mixed bundle;
- explicit actors and relationships;
- dates and temporal order;
- enough contrast between stakeholders;
- no private data that should not live in a public repository.

If you need help, use `references/seed-templates.md`.

## Step 3: Prepare A Pilot Run

Do not start with your largest budget run.

Start with:

- a smaller scenario;
- fewer rounds;
- one known-good model route;
- the minimum changes needed to test the question.

The pilot exists to answer: "Is this setup producing meaningful artifacts at all?"

## Step 4: Inspect The First Artifacts

Before scaling, inspect:

- `state.json`
- `simulation_config.json`
- generated profiles
- per-platform `actions.jsonl`
- `run_state.json`

Look for:

- coherent entities;
- distinct personas;
- actions that keep evolving after initialization;
- a config that matches the scenario you asked for.

If those are weak, stop there. Do not spend more budget on the same setup.

## Step 5: Decide Whether To Scale

Scale only if the pilot shows:

- sensible entities and profiles;
- more than trivial startup actions;
- evidence that the route can survive runtime and report stages;
- a report that can be audited against raw artifacts.

If you scale, change only one major variable at a time:

- model route;
- source material;
- requirement wording;
- rounds;
- agent count.

## Step 6: Audit The Report

Treat `report.md` as a summary layer.

For any important claim:

1. find the claim in `report.md`;
2. verify support in `twitter/actions.jsonl` or `reddit/actions.jsonl`;
3. inspect `agent_log.jsonl` to see how the report agent reasoned;
4. classify the claim using `references/evidence-taxonomy.md`.

If the report sounds strong but the artifacts are weak, trust the artifacts.

## Step 7: Score The Run

Use `references/evaluation-rubric.md` to score:

- simulation quality;
- report quality.

That gives you a comparable record across runs instead of vague impressions like "seemed better."

## Step 8: Record What Changed

For each run, log:

- model and route;
- main variable changed;
- rounds and action count;
- artifacts checked;
- simulation score;
- report score;
- one clear takeaway.

Use `references/experiment-protocol.md` if the run is part of a comparison.

## Mid-Run Checks That Save Budget

Do these before a long run finishes:

- inspect action growth around the first meaningful rounds;
- stop early if actions are repetitive or near-empty;
- stop early if the UI says "running" but files stopped changing;
- stop early if the model route is failing structured outputs.

## When To Use Deep Interaction

Use interviews or follow-up interaction after you already have:

- a complete simulation;
- a report worth auditing;
- one specific uncertainty you want to probe.

Do not use interaction as a substitute for weak source material or a broken run.
