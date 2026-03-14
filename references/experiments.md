# MiroFish Experiments Log

Real-world experiment results to help you calibrate expectations and avoid known pitfalls.

## Experiment 1 — Small Model, BTC Prediction (20 rounds)

- **Model**: Gemini Flash (free tier)
- **Rounds**: 20, ~116 actions
- **Result**: Brief output, limited depth. Free tier rate limits (15 RPM) slowed generation
- **Lesson**: Small/free models are too shallow for meaningful prediction reports

## Experiment 2 — Small Model, BTC Prediction (30 rounds)

- **Model**: Gemini Flash (free tier)
- **Rounds**: 30, ~187 actions
- **Report**: Generated successfully
- **Lesson**: More rounds = more data for report, but a weak model still produces surface-level analysis

## Experiment 3 — Large Model, BTC Prediction (10 rounds)

- **Model**: Claude Opus 4 (via API)
- **Rounds**: 10, ~134 actions
- **Cost**: ~$9-10 per run
- **Quality**: Dramatically better — deeper reasoning, richer agent interactions
- **Lesson**: Model quality matters enormously for both simulation and report depth
- **⚠️ OOM risk**: 10 rounds is safe limit with large models on 8GB RAM. More rounds may crash.

## Experiment 4 — Large Model via Proxy, BTC Prediction (10 rounds)

- **Model**: GPT-5 class (via OpenAI-compatible proxy, $0 cost)
- **Rounds**: 10, only 8 actions (4 reddit + 4 twitter initial posts)
- **Issue**: Simulation completed in 1.7 seconds — agents didn't make LLM calls during rounds
- **Root cause**: OASIS engine creates initial posts but may not invoke LLM for per-round reasoning
- **Report**: Generated successfully after fixing proxy compatibility issues

### Bugs Discovered and Fixed

1. **Assistant content type**: OpenAI Responses API requires `output_text` for assistant messages, not `input_text`. If you use a custom proxy, ensure this mapping is correct.
2. **Environment propagation**: `run_parallel_simulation.py` subprocess may not inherit parent Flask env vars if `load_dotenv()` overrides them. Fix: ensure `.env` file has correct values, or modify `simulation_runner.py` to use `os.environ` directly.
3. **Backend venv**: Must use `.venv/bin/python3`, not system python (Flask and deps are in venv only).

## Key Observations Across All Experiments

### Agent Generation
- MiroFish extracts entities from seed text via Zep GraphRAG
- Each entity becomes an agent with auto-generated persona (500-2000 chars)
- For a BTC prediction seed, typical agents generated: regulatory bodies (SEC, EU MiCA), technical analysts (RSI, MA, Fibonacci), institutional actors (Mt.Gox, exchanges)
- Personas are generated in Chinese by default (MiroFish's native language) — works fine regardless of seed text language

### Simulation Behavior
- Initial posts are generated during setup (typically 4 Twitter + 4 Reddit)
- Rounds may NOT involve per-agent LLM calls — OASIS engine can operate on pre-computed behavior
- "20 rounds" doesn't necessarily mean "20 × N_agents LLM calls"
- Actual LLM usage depends on OASIS engine internals

### Report Generation
- This is where most LLM calls happen (dozens of multi-turn conversations)
- ReportAgent uses ReACT: plans sections → researches via Zep → writes → reflects
- Report quality directly correlates with model quality
- Multi-turn conversations (3-7 messages per section) are common

### Cost Comparison

| Model Tier | Approx. Cost | Quality | Speed |
|-----------|-------------|---------|-------|
| Free/small (Gemini Flash, Qwen-turbo) | ~$0 | Low | Fast |
| Mid-range (GPT-4o, Claude Sonnet) | ~$2-5 | Medium | Medium |
| Large (GPT-4+, Claude Opus) | ~$8-12 | High | Slow |
| Via subscription proxy | $0 (covered by subscription) | High | Medium |
