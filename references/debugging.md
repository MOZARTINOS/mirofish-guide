# MiroFish Debugging Reference

Use this file when the task is operational: setup failures, weak outputs, missing files, empty simulations, or confusing report behavior.

Unless stated otherwise, file paths in this document refer to a local checkout of the upstream `MiroFish` engine repository.

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
- `backend/uploads/simulations/<simulation_id>/actions.jsonl`
- `backend/uploads/simulations/<simulation_id>/env_status.json`

For a report:

- `backend/uploads/reports/<report_id>/agent_log.jsonl`
- `backend/uploads/reports/<report_id>/console_log.txt`

If those files are missing or obviously incomplete, do not start by editing prompts. Fix the broken stage first.

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

Do not assume persona problems are caused by OASIS itself.

## Symptom: Simulation Finishes Too Fast

This often means the runtime did not perform much meaningful per-round reasoning.

Check:

- `run_state.json`
- `actions.jsonl`
- whether only initial posts were created
- whether the environment stayed alive long enough to accumulate actions

Important interpretation:

- more rounds do not guarantee proportionally more LLM reasoning;
- runtime behavior can rely heavily on pre-generated profiles and environment logic.

## Symptom: Proxy Or OpenAI-Compatible Endpoint Misbehaves

Known issue pattern:

- assistant message content type compatibility can break custom proxies;
- some setups need assistant content mapped as `output_text` rather than `input_text`

When a proxy is involved:

- verify request and response formats against the OpenAI-compatible layer you are using;
- separate transport-format failures from actual model-quality failures.

## Symptom: Report Quality Is Weak

Report quality is often the last visible symptom, not the first root cause.

Check in order:

1. Was the source material strong enough?
2. Did the graph contain the right entities?
3. Did the profiles contain useful personas?
4. Did the simulation produce enough actions?
5. What do `agent_log.jsonl` and `console_log.txt` show?

If the report logs show shallow tool usage or poor section reasoning, model quality is a plausible bottleneck.

## Symptom: Environment State Looks Stuck

Check:

- `env_status.json`
- `run_state.json`
- whether the backend process can still reach the simulation environment

The engine exposes environment-status and close-environment flows. Use state inspection before force-stopping processes.

## Evidence Discipline

When documenting a problem in this guide repository, always label it as one of:

- code-confirmed
- artifact-confirmed
- experiment-confirmed
- hypothesis

That one habit keeps the repository trustworthy as upstream MiroFish evolves.
