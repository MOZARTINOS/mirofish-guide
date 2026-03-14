# Contributing to MiroFish Guide

This repository is a companion guide for the MiroFish engine. Contributions should make the guide more useful for operators and AI agents, not just longer.

## What We Want Most

1. `Code-grounded notes`
   Add guidance tied to actual MiroFish files, generated artifacts, or API behavior.

2. `Experiment logs`
   Record real runs with model, rounds, action counts, failures, and takeaways.

3. `Prompt and seed templates`
   Add reusable input patterns for real MiroFish scenarios.

4. `Version drift updates`
   If upstream MiroFish changes behavior, update this guide and name the affected stage.

## Evidence Standard

When you add a claim, label it with the evidence taxonomy from `references/evidence-taxonomy.md`:

- code-confirmed
- doc-confirmed
- artifact-confirmed
- experiment-confirmed
- analogy-based
- unresolved

Only clearly labeled evidence should appear in the guide. Do not present analogy-based guidance as engine fact.

## How To Submit

1. Fork the repo.
2. Create a branch.
3. Make the smallest useful change that improves the guide.
4. Submit a PR that states:
   - what changed;
   - which pipeline stage it affects;
   - which evidence label applies;
   - which artifacts or code paths you checked.

## Experiment Log Format

When adding experiments to `references/experiments.md`, use the protocol in `references/experiment-protocol.md` and keep the summary compact:

```markdown
## Experiment N: [Model], [Scenario], [Rounds]

- `Model`: ...
- `Rounds`: ...
- `Actions`: ...
- `Result`: ...
- `Takeaway`: ...
- `Simulation score`: ...
- `Report score`: ...
- `Artifacts checked`: ...
```

## Style Rules

- keep it practical and reproducible;
- prefer artifact paths and concrete numbers over vague claims;
- document failures, not just success cases;
- change one main variable at a time when possible;
- do not include secrets, personal data, or internal-only endpoints.
