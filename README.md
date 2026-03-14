# 🐟 MiroFish Guide

> Practical usage guide for [MiroFish](https://github.com/666ghj/MiroFish) — the open-source swarm intelligence prediction engine.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![MiroFish](https://img.shields.io/badge/MiroFish-v1.0-blue)](https://github.com/666ghj/MiroFish)
[![OpenClaw Skill](https://img.shields.io/badge/OpenClaw-Skill-orange)](https://github.com/openclaw/openclaw)

## Why This Guide?

MiroFish is a powerful multi-agent simulation engine, but it ships without a practical "how to get good results" guide. This skill fills that gap — based on real experiments, not theory.

## What's Covered

| Topic | Description |
|-------|-------------|
| **Seed Text Design** | How to write effective seed texts for entity extraction |
| **Agent Roles** | Understanding auto-generated personas (MBTI, stance, influence) |
| **Simulation Tuning** | Rounds, activity levels, OOM prevention |
| **Report Analysis** | Working with ReportAgent and Zep tools |
| **LLM Configuration** | Model selection, proxy setup, cost optimization |
| **Common Pitfalls** | Bugs and gotchas discovered through real usage |
| **Experiment Logs** | Real results comparing models, rounds, and configurations |

## Quick Start

### As an OpenClaw Skill

```bash
# Install the skill
openclaw skill install mirofish-guide.skill

# The skill auto-activates when you work with MiroFish
```

### Manual Usage

Just read [`SKILL.md`](SKILL.md) — it's a standalone guide. The [`references/experiments.md`](references/experiments.md) file has detailed experiment logs.

## Structure

```
mirofish-guide/
├── SKILL.md                    # Main guide (seed text, agents, tuning, pitfalls)
├── references/
│   └── experiments.md          # Real experiment logs with different models/configs
├── README.md
└── LICENSE
```

## Key Takeaways (TL;DR)

1. **Seed text quality > everything else** — detailed, multi-stakeholder text with named entities produces the best agents
2. **Model quality matters enormously** — GPT-4+ / Claude Opus produce dramatically better reports than free-tier models
3. **More agents ≠ better** — 9 focused agents with diverse stances beat 50 generic ones
4. **Report generation is where the magic happens** — simulations may be quick, but reports use dozens of LLM calls
5. **10 rounds is the safe limit** for large models on 8GB RAM

## Contributing

Contributions welcome! Areas that need work:

- [ ] More experiment logs with different use cases (politics, product launches, public opinion)
- [ ] Seed text templates for common scenarios
- [ ] Agent tuning strategies (manual persona overrides)
- [ ] OASIS engine deep dive (when does it actually make LLM calls per round?)
- [ ] Multi-language seed text comparison
- [ ] Cost optimization strategies

### How to Contribute

1. Fork this repo
2. Add your experiments to `references/experiments.md`
3. Update `SKILL.md` with new findings
4. Submit a PR with a description of what you tested and learned

## Related

- [MiroFish](https://github.com/666ghj/MiroFish) — the simulation engine itself
- [OASIS](https://github.com/camel-ai/oasis) — underlying social simulation framework
- [OpenClaw](https://github.com/openclaw/openclaw) — AI assistant platform (skills system)
- [Zep](https://www.getzep.com/) — memory/graph service used by MiroFish

## License

MIT — use freely, contribute back if you can.
