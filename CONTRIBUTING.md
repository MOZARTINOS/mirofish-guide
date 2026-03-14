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

When you add a claim, label it mentally as one of:

- code-confirmed
- artifact-confirmed
- experiment-confirmed
- hypothesis

Only the first three belong in the guide without a warning label.

## How To Submit

1. Fork the repo.
2. Create a branch.
3. Make the smallest useful change that improves the guide.
4. Submit a PR that states:
   - what changed;
   - which pipeline stage it affects;
   - whether the change is code-confirmed or experiment-confirmed.

## Experiment Log Format

When adding experiments to `references/experiments.md`, use a compact format:

```markdown
## Experiment N: [Model], [Scenario], [Rounds]

- `Model`: ...
- `Rounds`: ...
- `Actions`: ...
- `Result`: ...
- `Takeaway`: ...
```

## Style Rules

- keep it practical and reproducible;
- prefer artifact paths and concrete numbers over vague claims;
- document failures, not just success cases;
- do not include secrets, personal data, or internal-only endpoints.
