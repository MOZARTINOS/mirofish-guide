# MiroFish Experiments Log

These notes are empirical. Treat them as run observations, not engine guarantees.

For code-grounded defaults and file paths, use:

- `references/workflow.md`
- `references/debugging.md`
- `references/experiment-protocol.md`
- `references/evaluation-rubric.md`

## Cross-Run Patterns

Patterns that consistently showed up in experiments:

- source material quality dominated downstream quality;
- model quality mattered much more for report depth than for raw runtime speed;
- round count alone was a poor proxy for actual reasoning depth;
- artifact inspection was more reliable than guessing from the final report text.

## Experiment 1: Small Model, BTC Prediction, 20 Rounds

- `Model`: Gemini Flash, free tier
- `Rounds`: 20
- `Actions`: about 116
- `Result`: shallow report, slow generation because of free-tier limits
- `Takeaway`: free or very small models can finish the pipeline, but the report usually stays superficial

## Experiment 2: Small Model, BTC Prediction, 30 Rounds

- `Model`: Gemini Flash, free tier
- `Rounds`: 30
- `Actions`: about 187
- `Result`: the report completed, but depth stayed limited
- `Takeaway`: extra rounds can add more data, but they do not compensate for a weak model

## Experiment 3: Large Model, BTC Prediction, 10 Rounds

- `Model`: Claude Opus 4 via API
- `Rounds`: 10
- `Actions`: about 134
- `Estimated cost`: about `$9-10` per run
- `Result`: much stronger reasoning and more convincing report sections
- `Takeaway`: better models improve both persona richness and report quality
- `Risk`: on an `8 GB` machine, 10 rounds was the practical ceiling before memory risk became noticeable

## Experiment 4: Large Model Via Proxy, BTC Prediction, 10 Rounds

- `Model`: GPT-5-class model through an OpenAI-compatible proxy
- `Rounds`: 10
- `Actions`: only 8 initial actions across both platforms
- `Result`: runtime finished almost immediately, then report generation succeeded after proxy fixes
- `Takeaway`: a completed run does not necessarily mean meaningful per-round reasoning happened

## Experiment-Confirmed Failure Patterns

1. `Assistant content type mismatch`
   Some OpenAI-compatible layers expect assistant output as `output_text`. A mismatch can break runs even when the model itself is fine.

2. `Environment variable override confusion`
   Root `.env` loading with override semantics can defeat values injected by a parent Flask process or wrapper script.

3. `Backend interpreter mismatch`
   Running outside the managed virtual environment caused dependency and startup problems.

## Cost Heuristic

| Model tier | Approx. cost | Quality | Speed |
|-----------|--------------|---------|-------|
| Free or small | `$0` | Low | Fast |
| Mid-range | `$2-5` | Medium | Medium |
| Large frontier model | `$8-12` | High | Slow |
| Subscription-backed proxy | Varies | Medium to high | Medium |

## Logging Discipline For Future Experiments

When you add new experiments, record:

- model name and route type
- round count
- action count
- whether runtime behavior looked substantive
- whether report generation succeeded
- cost estimate
- simulation score from `references/evaluation-rubric.md`
- report score from `references/evaluation-rubric.md`
- the artifact paths you actually checked
- the single most useful takeaway
