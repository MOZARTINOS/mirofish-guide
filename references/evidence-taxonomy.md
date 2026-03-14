# MiroFish Evidence Taxonomy

Use this file when deciding how strongly to word a claim in this repository or a conclusion drawn from a MiroFish run.

## Repository Claim Levels

Use these labels in documentation and issue discussions.

| Label | Meaning | Typical source |
|-------|---------|----------------|
| `code-confirmed` | Verified directly in the upstream MiroFish codebase | source files, config defaults, API handlers |
| `doc-confirmed` | Stated in public upstream documentation or official demos | README, docs, issue comments from maintainers |
| `artifact-confirmed` | Verified from generated runtime or report artifacts | `state.json`, `run_state.json`, `actions.jsonl`, `agent_log.jsonl` |
| `experiment-confirmed` | Observed in one or more real runs and logged clearly | experiment logs, run comparisons |
| `analogy-based` | Borrowed from adjacent systems and adapted cautiously | OASIS, Zep, GraphRAG, multi-agent eval literature |
| `unresolved` | Plausible but not yet verified enough to present as guidance | open questions, missing upstream details |

## Simulation Output Levels

Use these labels when interpreting a specific simulation result.

| Level | Label | Meaning |
|-------|-------|---------|
| `E1` | Convergent multi-run | Same pattern appears across multiple comparable runs |
| `E2` | Single-run emergent | Interesting pattern appears in one run only |
| `E3` | Report-asserted | The report claims it, but raw evidence has not been checked yet |
| `E4` | Agent-stated | A simulated agent claims it during interview or dialogue |
| `E5` | Operator inference | A human infers it without sufficient simulation evidence |

## Decision Rules

- Prefer `code-confirmed`, `doc-confirmed`, and `artifact-confirmed` claims in core guide files.
- Treat `experiment-confirmed` findings as useful but contingent on run conditions.
- Keep `analogy-based` guidance clearly labeled so it does not masquerade as native MiroFish behavior.
- Never present `unresolved` items as settled best practice.

## Verification Workflow

1. Check whether the claim can be proven from code.
2. If not, check public upstream docs or maintainer statements.
3. If not, inspect generated artifacts from a real run.
4. If not, check whether repeated experiments support it.
5. If still uncertain, downgrade it to `analogy-based` or `unresolved`.

## Example Usage

- "MiroFish loads config from the project root `.env` with override semantics." -> `code-confirmed`
- "Large-model runs can become expensive quickly." -> `experiment-confirmed`
- "Temporal anchoring likely improves graph quality because the underlying memory layer is temporal." -> `analogy-based`
- "This run proves the real world will behave the same way." -> invalid claim

## Writing Standard For This Repository

When in doubt, use weaker language.

- Strong wording: use for `code-confirmed` and `artifact-confirmed`
- Moderate wording: use for `experiment-confirmed`
- Conditional wording: use for `analogy-based`
- Explicit uncertainty: use for `unresolved`
