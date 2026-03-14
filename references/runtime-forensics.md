# MiroFish Runtime Forensics

Use this file when a simulation technically "ran" but you need to decide whether it actually produced meaningful behavior.

## Primary Evidence Sources

Check these before trusting any final report:

- `state.json`
- `simulation_config.json`
- `run_state.json`
- `twitter/actions.jsonl`
- `reddit/actions.jsonl`
- `twitter_simulation.db`
- `reddit_simulation.db`

## Core Questions

Ask these in order:

1. Did both enabled platforms actually start?
2. Did rounds advance beyond initialization?
3. Did multiple agents act, or only a tiny subset?
4. Did the action mix evolve over time?
5. Do files keep changing even if the UI looks stuck?

## Signs Of A Healthy Run

- both platforms produce actions if both were enabled;
- action counts keep increasing over meaningful rounds;
- more than one or two agents appear repeatedly;
- the action mix is not just startup posts or idle behavior;
- database files exist and are readable.

## Signs Of A Trivial Or Misleading Run

- only a few startup actions exist;
- one platform is effectively silent;
- the run ends quickly with little or no round progression;
- the report exists, but raw artifacts are thin;
- the UI says "running" while logs stop changing.

## File-First Checklist

### `run_state.json`

Check:

- configured rounds;
- current rounds;
- stopped or completed status;
- any mismatch between expected and actual progress.

### Per-platform `actions.jsonl`

Check:

- whether actions continue after initialization;
- which agents appear most often;
- whether the last actions are recent and varied;
- whether one platform never really joined the run.

### SQLite databases

First introspect the database instead of assuming table names:

```sql
SELECT name
FROM sqlite_master
WHERE type = 'table'
ORDER BY name;
```

Then inspect whichever action, post, comment, or trace tables actually exist in your run.

## Stop-Early Conditions

Stop the run and fix inputs or route quality if:

- action growth stalls early;
- both platforms look repetitive or incoherent;
- only initialization artifacts are present;
- the model route keeps failing structured output or status updates.

## Practical Classification

Classify the runtime before you move on to report analysis:

- `healthy`: sustained multi-agent behavior, usable evidence
- `partial`: some evidence exists, but one platform or one stage is weak
- `trivial`: technically completed, but too little happened to trust the report

If the run is `partial` or `trivial`, document that explicitly.
