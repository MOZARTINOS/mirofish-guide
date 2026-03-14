# MiroFish Glossary

Use this file when you need short definitions without opening the full stage references.

## MiroFish

The multi-stage engine that turns source material into a graph, agent profiles, simulations, and a final report.

## Source Material

The uploaded `pdf`, `md`, `txt`, or `markdown` files that seed the graph and constrain everything downstream.

## Graph Build

The stage that chunks source text, sends it into Zep, and produces the graph structure used later for entities and context.

## Entity Filtering

The step that decides which extracted entities become serious simulation candidates.

## OASIS

The social-simulation framework MiroFish uses for runtime behavior across Twitter-like and Reddit-like environments.

## Zep

The graph and memory service used by MiroFish for graph-backed context and longer-lived memory structures.

## GraphRAG

The general idea of using graph structure, not only plain embeddings, to retrieve and organize knowledge.

## Simulation Requirement

The operator-written instruction that tells MiroFish what scenario to explore, over what timeframe, and with which focus.

## Temporal Anchoring

Making dates, ordering, and state changes explicit so the graph and agents do not blur time-dependent facts together.

## `state.json`

The high-level simulation state file used to track overall stage progress.

## `run_state.json`

The runtime-state file that reflects live simulation progress and stop conditions.

## `env_status.json`

The environment-status file used to inspect whether the simulation environment is still alive and reachable.

## `actions.jsonl`

The per-platform action log. This is one of the primary evidence files for deciding whether a run actually produced meaningful behavior.

## `agent_log.jsonl`

The structured report-agent log. Use it to audit tool calls and reasoning flow during report generation.

## `insight_forge`

One of the report-stage tools for deeper graph-backed analysis.

## `interview_agents`

One of the report-stage tools for querying simulated agents directly from the report workflow.

## Evidence Taxonomy

The label system in `references/evidence-taxonomy.md` used to separate code-confirmed facts from experiments, analogies, and unresolved claims.
