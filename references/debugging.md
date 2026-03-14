# MiroFish Debugging Reference

Use this file when the task is operational: setup failures, weak outputs, missing files, empty simulations, or confusing report behavior.

Unless stated otherwise, file paths in this document refer to a local checkout of the upstream `MiroFish` engine repository.

For evidence labels and report-claim verification, also read:

- `references/evidence-taxonomy.md`
- `references/evaluation-rubric.md`

## Environment Sanity Checks

MiroFish expects its core configuration in the project root `.env`.

Required keys:

- `LLM_API_KEY`
- `ZEP_API_KEY`

Important defaults:

- `LLM_BASE_URL` defaults to `https://api.openai.com/v1`
- `LLM_MODEL_NAME` defaults to `gpt-4o-mini`
- `OASIS_DEFAULT_MAX_ROUNDS` defaults to `10`

Important behavior:

- config loading uses `load_dotenv(..., override=True)`
- that means values from the root `.env` can override values passed in from a parent process

If behavior looks inconsistent across shell, Flask, and subprocesses, inspect `.env` first.

## Recommended Startup Path

Use the repository scripts instead of ad hoc commands:

- `npm run setup:all`
- `npm run dev`
- `npm run backend`
- `npm run frontend`

For backend-only runs, prefer the managed virtualenv flow (`uv run python run.py`) rather than system Python.

## Generated Files To Inspect First

For a simulation:

- `backend/uploads/simulations/<simulation_id>/state.json`
- `backend/uploads/simulations/<simulation_id>/simulation_config.json`
- `backend/uploads/simulations/<simulation_id>/reddit_profiles.json`
- `backend/uploads/simulations/<simulation_id>/twitter_profiles.csv`
- `backend/uploads/simulations/<simulation_id>/run_state.json`
- `backend/uploads/simulations/<simulation_id>/env_status.json`
- `backend/uploads/simulations/<simulation_id>/twitter/actions.jsonl`
- `backend/uploads/simulations/<simulation_id>/reddit/actions.jsonl`
- `backend/uploads/simulations/<simulation_id>/twitter_simulation.db`
- `backend/uploads/simulations/<simulation_id>/reddit_simulation.db`

For a report:

- `backend/uploads/reports/<report_id>/agent_log.jsonl`
- `backend/uploads/reports/<report_id>/console_log.txt`
- `backend/uploads/reports/<report_id>/report.md`
- `backend/uploads/reports/<report_id>/report_outline.json`

If those files are missing or obviously incomplete, do not start by editing prompts. Fix the broken stage first.

## Quick Triage Order

When a run looks wrong, check in this order:

1. `state.json` and `simulation_config.json`
2. filtered entities and generated profiles
3. per-platform `actions.jsonl`
4. `run_state.json` and `env_status.json`
5. per-platform SQLite databases
6. `agent_log.jsonl`
7. final `report.md`

That order prevents you from treating the report as the source of truth.

## Symptom: Graph Built Poorly

Likely causes:

- source material too vague or too short;
- missing named entities;
- too many unrelated topics in one document;
- ontology mismatch or weak extraction.

Check:

- graph build task status
- resulting entity count and entity types
- whether the source document actually contains usable facts and relationships

Useful fixes:

- add explicit dates, actors, and relationship statements;
- split mixed scenarios into separate source packages;
- normalize contradictory or superseded facts instead of leaving them implicit;
- retry with a route that is more reliable at structured JSON.

Known upstream issue-tracker patterns to keep in mind:

- free-tier Zep usage can hit `429` rate limits during ingestion;
- stricter graph tooling can reject badly normalized entity targets.

Treat those as reproducibility hints until you confirm them in your own run.

## Symptom: Personas Are Generic

Likely causes:

- weak extracted entities;
- thin source context;
- low-quality model for profile generation;
- irrelevant entity types surviving filtering.

Check:

- filtered entity list first
- then `reddit_profiles.json` and `twitter_profiles.csv`
- then simulation requirement wording
- then whether source text gave each actor enough context to differ from the others

Do not assume persona problems are caused by OASIS itself.

## Symptom: Simulation Finishes Too Fast

This often means the runtime did not perform much meaningful per-round reasoning.

Check:

- `run_state.json`
- `twitter/actions.jsonl`
- `reddit/actions.jsonl`
- `twitter_simulation.db`
- `reddit_simulation.db`
- whether only initial posts were created
- whether the environment stayed alive long enough to accumulate actions

Important interpretation:

- more rounds do not guarantee proportionally more LLM reasoning;
- runtime behavior can rely heavily on pre-generated profiles and environment logic.

Operator response:

1. stop treating the run as valid evidence;
2. inspect whether actions plateaued after setup;
3. compare action diversity, not just action count;
4. rerun with a smaller scenario and a stronger model or cleaner proxy route.

## Symptom: The UI Still Says "Running"

The frontend polling logic in `frontend/src/components/Step3Simulation.vue` mainly treats `completed` and `stopped` as terminal runtime states and only logs fetch failures to the console.

That means a backend crash or broken status fetch can look like a stuck run from the UI.

Check:

- backend terminal output first;
- `run_state.json`
- `state.json`
- `env_status.json`
- whether `twitter/actions.jsonl` or `reddit/actions.jsonl` stopped growing

If the UI and files disagree, trust the files.

## Symptom: Proxy Or OpenAI-Compatible Endpoint Misbehaves

Known issue pattern:

- assistant message content type compatibility can break custom proxies;
- some setups need assistant content mapped as `output_text` rather than `input_text`

When a proxy is involved:

- verify request and response formats against the OpenAI-compatible layer you are using;
- separate transport-format failures from actual model-quality failures.

Reject a route for serious runs if it repeatedly fails any of these checks:

- returns malformed JSON during graph or config generation;
- produces near-empty runtime action logs;
- fails on tool-heavy report generation;
- hides useful error information behind generic HTTP success responses.

## Symptom: Report Quality Is Weak

Report quality is often the last visible symptom, not the first root cause.

Check in order:

1. Was the source material strong enough?
2. Did the graph contain the right entities?
3. Did the profiles contain useful personas?
4. Did the simulation produce enough actions?
5. What do `agent_log.jsonl` and `console_log.txt` show?

If the report logs show shallow tool usage or poor section reasoning, model quality is a plausible bottleneck.

Direct upstream code check:

- the report agent caps section tool calls at `5`;
- its section-generation prompt demands at least `3` tool calls before writing a final section.

Practical implication:

- if the log shows too few useful tool calls, repeated tool calls with no new information, or weak observations, the report stage was underpowered even if the final markdown looks polished.

## Report Audit Checklist

Before trusting a report claim, verify:

1. the claim appears in `report.md`;
2. supporting actions exist in `twitter/actions.jsonl` or `reddit/actions.jsonl`;
3. the platform databases contain compatible aggregate evidence;
4. `agent_log.jsonl` shows which tools the report agent used;
5. the claim can be classified with an evidence level from `references/evidence-taxonomy.md`.

## Symptom: Environment State Looks Stuck

Check:

- `env_status.json`
- `run_state.json`
- whether the backend process can still reach the simulation environment

The engine exposes environment-status and close-environment flows. Use state inspection before force-stopping processes.

## Evidence Discipline

When documenting a problem in this guide repository, use the evidence labels defined in `references/evidence-taxonomy.md`.
