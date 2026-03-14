# MiroFish Model And Proxy Guidance

Use this file when testing models, OpenAI-compatible routes, or proxy layers for MiroFish.

## What Upstream Code Confirms

- `LLM_BASE_URL` is configurable through the root `.env`.
- the backend default `LLM_MODEL_NAME` is `gpt-4o-mini`.
- the upstream README examples recommend `qwen-plus`.
- report generation is a tool-backed stage, so weak reasoning routes usually fail there first.

## Route Acceptance Checklist

Reject a route for serious work if it cannot pass all of these:

1. graph build completes without malformed structured output;
2. entity and profile generation look coherent;
3. runtime produces meaningful per-platform actions;
4. report generation completes with useful tool-backed reasoning;
5. error cases are inspectable instead of silently swallowed.

## Common Failure Patterns

### Structured output failures

Symptoms:

- graph or config generation fails;
- JSON is malformed or incomplete;
- personas become generic because upstream structure was weak.

Response:

- test the route on a small scenario first;
- prefer routes that are reliable at JSON-heavy stages;
- do not blame MiroFish before validating the model route.

### Proxy content-type mismatch

Experiment-confirmed pattern:

- some OpenAI-compatible layers expect assistant content as `output_text` rather than `input_text`.

Response:

- inspect the exact request and response schema;
- separate transport compatibility from model quality.

### Cheap route, shallow report

Symptoms:

- runtime finishes;
- report exists;
- report tool usage is repetitive or low-value.

Response:

- inspect `agent_log.jsonl`;
- compare report scores, not just completion status.

## Compatibility Matrix Template

Use this table in PRs, issues, or local notes when comparing routes.

| Route | Model | Graph build | Runtime | Report | Structured JSON reliability | Notes | Evidence |
|------|-------|-------------|---------|--------|-----------------------------|-------|----------|
| Example | qwen-plus | pass | pass | pass | high | good default baseline | doc-confirmed plus local test |

## What To Measure

For each route, record:

- graph-build success rate;
- profile quality;
- total and per-platform action counts;
- whether actions remain meaningful after initialization;
- report score from `references/evaluation-rubric.md`;
- approximate cost and latency.

## Good Default Behavior

A route is a reasonable baseline when it:

- survives graph, runtime, and report stages;
- returns clean structured outputs consistently;
- does not collapse into empty actions;
- gives you debuggable failures when something breaks.

## Bad Signs

- repeated malformed JSON;
- near-empty action logs;
- platform mismatch where one side barely acts;
- report sections with weak or repetitive tool use;
- HTTP success responses that hide broken content.
