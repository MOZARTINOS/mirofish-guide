# MiroFish Experiments Log

## v1 — Gemini Flash, BTC prediction (20 rounds)

- **Project**: `proj_c8f04c1f3cd5`
- **Model**: Gemini Flash (free tier)
- **Rounds**: 20, 116 actions
- **Result**: Brief output, limited depth. Free tier rate limits (15 RPM) slowed generation
- **Lesson**: Gemini Flash too shallow for meaningful prediction reports

## v2 — Gemini Flash, BTC prediction (30 rounds)

- **Project**: `proj_cf7db7d150b9`
- **Rounds**: 30, 187 actions
- **Report**: `report_d3a82d6901e4` — generated successfully
- **Lesson**: More rounds = more data for report, but Gemini Flash still produces surface-level analysis

## v3 — Claude Opus 4, BTC prediction (10 rounds)

- **Project**: `proj_c1976801aed0`
- **Rounds**: 10, 134 actions
- **Report**: `report_056aca67f940`
- **Model cost**: ~$9-10 per run (Anthropic API)
- **Quality**: Dramatically better than Gemini Flash — deeper reasoning, richer agent interactions
- **Lesson**: Model quality matters enormously for both simulation and report depth
- **⚠️ OOM risk**: 10 rounds is safe limit with Opus on 8GB RAM server. More rounds may crash.

## v4 — GPT-5.4 via Codex Proxy, BTC prediction (10 rounds)

- **Project**: `proj_feaf8dff1372`
- **Rounds**: 10, only 8 actions (4 reddit + 4 twitter initial posts)
- **Model**: GPT-5.4 via Codex OAuth Proxy (port 4000, $0 cost)
- **Issue**: Simulation completed in 1.7 seconds — agents didn't make LLM calls during rounds
- **Root cause**: `run_parallel_simulation.py` loads `.env` which had correct config, but OASIS engine creates initial posts without per-round LLM reasoning
- **Fix applied**: Changed `env = os.environ.copy()` → `env = os.environ` in `simulation_runner.py`
- **Report attempt**: `report_b312eaccc9d0` — failed (Connection error when proxy restarted with API key)
- **Report v2**: `report_847388d0003b` — failed same reason
- **Report v3**: `report_828f74173b11` — generating, GPT-5.4 calls confirmed in proxy log

### Bugs discovered and fixed

1. **assistant content type**: Responses API requires `output_text` for assistant messages, not `input_text`. Error: `Invalid value: 'input_text'. Supported values are: 'output_text' and 'refusal'.`
2. **Environment propagation**: subprocess didn't inherit Flask env vars → `.env` values used instead
3. **Backend venv**: Must use `.venv/bin/python3`, not system python (Flask not in system packages)

## Key Observations Across All Experiments

### Agent Generation
- MiroFish extracts entities from seed text via Zep GraphRAG
- Each entity becomes an agent with auto-generated persona (500-2000 chars)
- BTC seed text produced: SEC, Mt.Gox, 200-day MA analyst, 50-day MA analyst, EU MiCA, RSI(14) analyst, Fibonacci analyst — all as separate agents
- Personas are generated in Chinese (MiroFish default language) — works fine regardless of seed text language

### Simulation Behavior
- Initial posts are generated during setup (4 Twitter + 4 Reddit typical)
- Rounds may NOT involve per-agent LLM calls — OASIS engine can operate on pre-computed behavior
- This means "20 rounds" doesn't mean "20 × N_agents LLM calls"
- Actual LLM usage depends on OASIS engine configuration

### Report Generation
- This is where most LLM calls happen (dozens of multi-turn conversations)
- ReportAgent uses ReACT: plans sections → researches via Zep → writes → reflects
- Report quality directly correlates with model quality
- Multi-turn conversations (3-7 messages) are common in report generation

### Cost Comparison
| Model | Cost per run | Quality | Speed |
|-------|-------------|---------|-------|
| Gemini Flash | ~$0 (free tier) | Low | Fast |
| Claude Opus 4 | ~$9-10 | High | Slow |
| GPT-5.4 (Codex Proxy) | $0 (subscription) | High | Medium |
