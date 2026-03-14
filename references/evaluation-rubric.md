# MiroFish Evaluation Rubric

Use this file to score a MiroFish run after simulation and report generation complete.

This rubric is intentionally operational. It is designed to answer:

- was the run mechanically healthy?
- was the emergent behavior interesting enough?
- was the report grounded in the simulation?
- is the result worth iterating on or trusting further?

## Simulation Quality

### Dimension 1: Agent Diversity

| Score | Criteria |
|-------|----------|
| `5` | Agents show clearly different personas, factions, and motivations |
| `4` | Most agents are distinct; some overlap exists but meaningful diversity remains |
| `3` | Basic diversity exists, but several agents feel interchangeable |
| `2` | Many agents converge too early or behave similarly |
| `1` | Agents are functionally homogeneous |

### Dimension 2: Emergent Behavior Richness

| Score | Criteria |
|-------|----------|
| `5` | Visible turning points, coalition shifts, polarization, or cascade effects |
| `4` | Clear evolution appears over time with identifiable dynamics |
| `3` | Some evolution occurs, but it stays predictable or shallow |
| `2` | Agents mostly repeat initial positions |
| `1` | The run is flat and mechanically repetitive |

### Dimension 3: Mechanical Integrity

| Score | Criteria |
|-------|----------|
| `5` | All stages complete cleanly; artifacts are coherent and usable |
| `4` | Minor issues appear, but outcomes remain usable |
| `3` | Manual retries or workarounds were needed |
| `2` | Significant failures affected outcome quality |
| `1` | The run crashed or produced unusable artifacts |

### Dimension 4: Resource Efficiency

| Score | Criteria |
|-------|----------|
| `5` | Time and cost stayed within expected bounds |
| `4` | Slightly above expected bounds, still acceptable |
| `3` | Roughly 2x expected time or cost |
| `2` | Significantly above expected time or cost |
| `1` | Resource usage was not viable for practical iteration |

## Report Quality

### Dimension 1: Factual Grounding

| Score | Criteria |
|-------|----------|
| `5` | Claims clearly trace to simulation artifacts or tool results |
| `4` | Mostly grounded, with minor generic phrasing |
| `3` | Mixed grounding; some claims are traceable, others are generic |
| `2` | Report relies heavily on generic LLM language |
| `1` | Report is largely detached from the simulation evidence |

### Dimension 2: Analytical Depth

| Score | Criteria |
|-------|----------|
| `5` | Identifies turning points, counterfactuals, minority positions, and causal chains |
| `4` | Explains main dynamics well and captures multiple perspectives |
| `3` | Adequate summary with limited second-order analysis |
| `2` | Superficial commentary with weak causal reasoning |
| `1` | Mostly generic summary or restatement |

### Dimension 3: Actionability

| Score | Criteria |
|-------|----------|
| `5` | Gives scenario-specific implications or decisions with clear conditions |
| `4` | Gives useful next-step guidance with some conditional framing |
| `3` | Provides moderate practical value |
| `2` | Mostly descriptive, weak for decision support |
| `1` | Not actionable |

### Dimension 4: Structure And Clarity

| Score | Criteria |
|-------|----------|
| `5` | Well organized, easy to scan, and internally consistent |
| `4` | Mostly clear, minor structural issues |
| `3` | Understandable but uneven |
| `2` | Hard to follow or redundant |
| `1` | Confusing or incomplete |

## Quick Scoring Sheet

| Dimension | Score | Notes |
|-----------|-------|-------|
| Agent Diversity | | |
| Emergent Behavior Richness | | |
| Mechanical Integrity | | |
| Resource Efficiency | | |
| Simulation Total | | `/20` |
| Factual Grounding | | |
| Analytical Depth | | |
| Actionability | | |
| Structure And Clarity | | |
| Report Total | | `/20` |
| Combined Total | | `/40` |

## Interpretation

- `30-40`: strong run worth documenting and comparing
- `24-29`: usable but should be iterated
- `16-23`: weak; inspect inputs, artifacts, and model choice
- `<16`: do not trust the output without major changes

## Suggested Evidence Attachments

When logging a scored run, attach:

- seed document identifier or hash
- exact simulation requirement text
- model and proxy route
- agent count and round count
- `actions.jsonl` summary
- report identifier and notable artifacts
