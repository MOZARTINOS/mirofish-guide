# MiroFish Graph Build Runbook

Use this file when the graph stage fails, hangs, returns sparse entities, or throws ontology-related errors.

For general stage mapping, also read:

- `references/workflow.md`
- `references/debugging.md`
- `references/seed-templates.md`

## What A Healthy Graph Stage Looks Like

A healthy graph build usually gives you:

- the main actors you expected;
- relationships that reflect the seed material;
- no flood of duplicate near-identical entities;
- enough context to support distinct profiles later.

If the graph is weak here, the rest of the pipeline inherits that weakness.

## Fast Triage

### Symptom: Graph build fails with `429`

Upstream issue tracker currently includes issue `#60` for Zep free-tier rate limiting during graph construction.

What to do:

- shrink the seed package;
- split one large source package into smaller focused documents;
- wait and retry instead of hammering the same request pattern;
- treat free-tier Zep runs as fragile for larger tests.

Evidence level:

- community-reported upstream issue;
- use `unresolved` until you reproduce it locally.

### Symptom: Graph build fails with PascalCase or target-name errors

Upstream issue tracker currently includes issue `#178` for graph build failure when entity names or targets are not normalized as expected.

What to do:

- keep actor names consistent in the source package;
- avoid duplicate aliases for the same actor;
- if you preprocess entities, normalize canonical labels before ingestion;
- remove noisy or malformed synthetic labels.

Evidence level:

- community-reported upstream issue;
- locally, treat it as `artifact-confirmed` only after matching the failure.

### Symptom: Ontology generation returns `500`

Upstream issue tracker currently includes issue `#180` for ontology-generation failures and active PRs around more robust JSON parsing.

Likely causes:

- route cannot return stable structured output;
- seed package is too noisy;
- local or proxy model is weak at JSON-heavy tasks.

What to do:

- switch to a route with more reliable structured output;
- simplify the seed package;
- rerun the graph stage before touching later stages.

## Source Package Rewrite Triggers

Rewrite the seed package before retrying if any of these are true:

- fewer than the main stakeholders appear in the graph;
- most entities are generic or duplicate variants;
- relationships are sparse or obviously wrong;
- the document mixes multiple unrelated events;
- dates or ordering are missing for a time-sensitive scenario.

## Acceptance Checklist

Do not proceed to profile generation until you can say yes to most of these:

- the graph contains the core actors;
- the core actors are named consistently;
- relationships are not obviously missing;
- there are enough entities to support distinct personas;
- the result matches the question you are actually simulating.

## Escalation Path

If repeated retries fail:

1. test a smaller seed with the same route;
2. test the same seed with a stronger route;
3. compare whether the failure is seed-driven or route-driven;
4. only then document it in the guide as an experiment or unresolved upstream issue.
