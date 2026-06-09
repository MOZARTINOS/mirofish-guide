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

## Known Fabrication Failure Modes (community-reported, 2026-06)

These are documented upstream failure modes, not hypotheticals. Verify against the live tracker — issue
numbers drift over time.

- issue `#529`: sections can contain plausible-sounding but **fabricated** entities, quotes, and
  statistics that never appeared in the simulation;
- issue `#599`: raw, **unexecuted `tool_call` JSON** can be written directly into a section the tracker
  still marks "completed" — a polished status does not mean the section was actually produced cleanly;
- issue `#492`: the pipeline does not fetch or validate against live real-world data, so a confident
  report can sit on "four layers of unverified assumptions."

Because there is no upstream accuracy benchmark, treat a MiroFish report as **qualitative narrative, not
a numeric forecast**. The audit below is what keeps a fabricated-but-fluent section from being cited as
fact. Background and the broader "plausible narrative, not validated prediction" framing:
`references/project-context.md`.

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
