---
name: mirofish-guide
description: "Guide for using MiroFish swarm intelligence prediction engine. Use when: creating MiroFish simulations, designing agent roles/personas, formulating seed texts, configuring simulation parameters, interpreting reports, or any MiroFish-related task. Covers seed text best practices, agent design (quantity, roles, MBTI, stance, influence), simulation tuning (rounds, activity, events), report analysis, and common pitfalls."
---

# MiroFish — Practical Usage Guide

MiroFish is a multi-agent social simulation engine. It builds a parallel digital world from seed data, populates it with AI agents, lets them interact on simulated Twitter/Reddit, and generates prediction reports from the emergent behavior.

**Key insight**: You don't configure agents manually. You provide **seed text** + **simulation topic** → MiroFish extracts entities from your text and auto-generates agent personas via LLM.

## Architecture (5 stages)

1. **Seed text** → Upload document (news, report, analysis, story)
2. **Knowledge Graph** → Zep Cloud extracts entities, relationships, builds GraphRAG
3. **Agent Generation** → LLM creates detailed personas from graph nodes (MBTI, stance, country, profession, sentiment, activity level)
4. **Simulation** → Agents post/comment/retweet on simulated Twitter + Reddit (OASIS engine)
5. **Report** → ReportAgent (ReACT pattern) analyzes simulation data via Zep tools, generates structured report

## How to Formulate a Good Seed Text

The seed text is the **most important input** — it determines what entities get extracted and what agents get created.

### Principles

- **Include all key stakeholders** as named entities (people, organizations, roles)
- **Include factual data** — numbers, dates, metrics (agents use these in reasoning)
- **Include multiple perspectives** — bullish/bearish, for/against, different countries
- **Include relationships** between entities ("SEC regulates exchanges", "analysts predict based on indicators")
- **Length**: 500-3000 words optimal. Too short = few entities. Too long = noise

### Seed Text Template

```
[CONTEXT PARAGRAPH]
Brief background of the topic. What happened, when, key facts and numbers.

[STAKEHOLDER SECTIONS — one per key actor]
[Actor Name]: Role, position, known stance, recent actions, typical behavior.
Include their relationships to other actors.

[DATA SECTION]
Key metrics, statistics, indicators relevant to the prediction.
Include recent trends and historical context.

[PREDICTION QUESTION]
What specifically should the simulation explore?
State the timeframe and scope clearly.
```

### Example (financial prediction)

Good seed text includes: regulatory bodies (SEC, EU MiCA), market indicators (RSI, MACD, moving averages), institutional actors (exchanges, funds), retail sentiment indicators, recent events with dates and numbers, and the specific prediction question.

### Anti-patterns

- ❌ Vague text: "Bitcoin might go up or down" → creates generic agents
- ❌ Single perspective: only bullish analysis → biased simulation
- ❌ No named entities: "some analysts think..." → weak graph extraction
- ❌ Too technical without context: raw data without explanation → agents can't reason about it

## Simulation Topic

The `simulation_topic` field guides what agents discuss. Be specific:

- ✅ "Bitcoin BTC price prediction for next 7-30 days. Current price $XX,XXX. Focus on: SEC regulatory impact, ETF flows, technical support levels, macro factors (CPI, Fed rate)."
- ❌ "What will happen with crypto?"

## Agent Design (Auto-Generated)

MiroFish auto-generates agents from graph entities. You influence agents indirectly through seed text quality. Each generated agent gets:

| Field | Description | Impact |
|-------|-------------|--------|
| `persona` | Detailed background (500-2000 chars) | Core behavior driver |
| `mbti` | Personality type (INTJ, ENFP, etc.) | Communication style |
| `stance` | supportive/opposing/neutral/observer | Position in debates |
| `sentiment_bias` | -1.0 to 1.0 | Positive/negative lean |
| `influence_weight` | 0.0 to 1.0+ | Visibility of posts |
| `activity_level` | 0.0 to 1.0 | Post frequency |
| `age`, `gender`, `country` | Demographics | Cultural perspective |

### How many agents?

- **5-10**: Fast, focused debate. Good for quick predictions
- **10-20**: Balanced — multiple perspectives without noise
- **20-50**: Rich ecosystem. Better for public opinion simulation
- **50+**: Expensive (LLM calls × agents × rounds). Use for large-scale sentiment

Agent count is determined by number of entities in your knowledge graph. More entities in seed text = more agents.

## Simulation Parameters

| Parameter | Default | Recommendation |
|-----------|---------|----------------|
| `num_rounds` | 10 | 10-30 for predictions, 50+ for deep opinion evolution |
| `max_rounds` | — | Set to prevent runaway simulations |

### Rounds vs Quality

- Fewer rounds (5-10): Quick snapshot, agents share initial positions
- Medium (10-30): Opinions start shifting, consensus/polarization emerges
- Many (30-100): Full opinion evolution, but expensive and may hit OOM

### OOM Prevention

- With large models (GPT-4+, Claude Opus): **max 10 rounds** on 8GB RAM server
- With small models (Gemini Flash, Qwen): 30+ rounds safe
- Monitor RAM during simulation — OASIS engine accumulates state

## Report Generation

ReportAgent uses ReACT pattern (Reason → Act → Observe → Repeat) with Zep tools:
- `search`: Search simulation data for specific topics
- `insight_forge`: Generate insights from agent interactions
- `panorama`: Overview of simulation state
- `interview`: "Interview" specific agents about their reasoning

Reports are generated section-by-section. Each section goes through multiple LLM reasoning cycles.

### Report Quality Depends On

1. **Model quality**: GPT-4+ / Claude Opus >> smaller models for report depth
2. **Simulation richness**: More rounds + more agents = richer data for report
3. **Topic specificity**: Vague topics = vague reports

## LLM Configuration

MiroFish supports any OpenAI SDK-compatible LLM API. Configure in `.env`:

```env
LLM_API_KEY=your_api_key
LLM_BASE_URL=https://api.openai.com/v1
LLM_MODEL_NAME=gpt-4o

ZEP_API_KEY=your_zep_api_key
```

Any OpenAI-compatible proxy (LiteLLM, Ollama, vLLM, etc.) works — just set `LLM_BASE_URL` accordingly.

## Common Pitfalls

1. **Simulation rounds ≠ LLM calls per round** — OASIS engine posts initial content but may not make LLM calls each round. Agents can act on pre-generated profiles without calling LLM.
2. **Report generation is where LLM shines** — ReportAgent makes many multi-turn LLM calls (dozens per report).
3. **More agents ≠ better** — 9 focused agents with diverse stances > 50 generic ones.
4. **Seed text quality > everything** — garbage in = garbage out.
5. **Backend needs venv** — use `.venv/bin/python3 run.py`, not system python.
6. **assistant message content type** — if using a custom proxy, ensure assistant messages use `output_text` (not `input_text`) in the Responses API format.
7. **Environment variable propagation** — `run_parallel_simulation.py` may call `load_dotenv()` which can override env vars set by the parent Flask process.

## Quick Start Checklist

1. [ ] Write seed text (500-3000 words, multiple stakeholders, data, relationships)
2. [ ] Formulate specific simulation_topic with timeframe
3. [ ] Configure LLM API in `.env`
4. [ ] Start MiroFish backend: `cd MiroFish/backend && .venv/bin/python3 run.py`
5. [ ] Start frontend: `cd MiroFish/frontend && npm run dev`
6. [ ] Create project → Upload seed → Build graph → Wait for graph completion
7. [ ] Start simulation (10-30 rounds recommended)
8. [ ] Generate report after simulation completes
9. [ ] Review report + optionally chat with ReportAgent or individual agents

## Experiment Notes

See [references/experiments.md](references/experiments.md) for detailed experiment logs showing how different models and configurations affect simulation quality.
