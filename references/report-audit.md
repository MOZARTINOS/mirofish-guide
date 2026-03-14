# MiroFish Report Audit

Use this file when deciding whether a MiroFish report is trustworthy enough to cite, compare, or document in this repository.

For evidence labels and scoring, also read:

- `references/evidence-taxonomy.md`
- `references/evaluation-rubric.md`

## Core Rule

Treat `report.md` as a summary layer.

The primary evidence lives in:

- per-platform `actions.jsonl`
- per-platform simulation databases
- `agent_log.jsonl`

## Audit Workflow

1. Read `report.md` and mark every concrete claim.
2. Find supporting runtime evidence in per-platform logs or databases.
3. Inspect `agent_log.jsonl` to see which tools the report agent actually used.
4. Classify each claim with an evidence level from `references/evidence-taxonomy.md`.
5. Downgrade any unsupported claim, no matter how polished the prose sounds.

## What To Check In `agent_log.jsonl`

Look for:

- total tool calls per section;
- whether the report agent used more than one useful tool;
- repeated tool calls that add no new evidence;
- whether interviews were used when the section needed first-person viewpoint;
- whether the section relied on real observations instead of generic synthesis.

Direct upstream code check:

- the section prompt requires at least `3` tool calls;
- the hard cap per section is `5`.

## Red Flags

- strong claims with no traceable artifact support;
- generic report language that could fit any scenario;
- no evidence of meaningful tool-backed analysis;
- unsupported causal claims;
- report conclusions that exceed what the runtime actually showed.

## Claim Audit Template

Use this table when reviewing an important report:

| Claim | Supporting artifact | Report tool evidence | Evidence level | Keep, downgrade, or reject |
|------|----------------------|----------------------|----------------|----------------------------|
| Example claim | `twitter/actions.jsonl` | `agent_log.jsonl` shows `insight_forge` | `E2` | keep with caution |

## When A Report Is Good Enough To Document

A report is worth documenting publicly when:

- the run itself was mechanically healthy;
- important claims can be traced back to artifacts;
- the analysis adds something beyond generic narrative;
- the evidence level is explicit.

If you cannot do that, log the run as exploratory instead of presenting it as a best-practice example.
