# Contributing to MiroFish Guide

Thanks for your interest in improving this guide! Here's how to help.

## What We Need Most

1. **Experiment logs** — Run MiroFish with different configurations and document results
2. **Seed text templates** — Create reusable templates for common prediction scenarios
3. **Bug reports** — Found a pitfall not documented? Add it
4. **Translations** — The guide is in English; translations welcome

## How to Submit

1. Fork the repo
2. Create a branch: `git checkout -b my-improvement`
3. Make your changes
4. Submit a PR with:
   - What you changed and why
   - If adding experiments: model used, rounds, agent count, results

## Experiment Log Format

When adding experiments to `references/experiments.md`, use this format:

```markdown
## Experiment N — [Model], [Topic] ([rounds] rounds)

- **Model**: [model name and tier]
- **Rounds**: [count], [action count] actions
- **Cost**: [approximate cost per run]
- **Quality**: [brief assessment]
- **Lesson**: [key takeaway]
```

## Style Guide

- Keep it practical — actionable advice over theory
- Include specific numbers (rounds, costs, action counts)
- Document failures too — what DIDN'T work is valuable
- No personal data, API keys, or internal URLs
