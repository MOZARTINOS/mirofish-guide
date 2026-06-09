# MiroFish Project Context

> **Snapshot dated 2026-06.** The rest of this guide is intentionally version-neutral so it does not
> rot as upstream MiroFish moves. This is the one file where dated, project-specific facts are allowed.
> If you are reading this much later, treat every number here as a point-in-time observation and
> re-check it against the live repository and issue tracker.

This file exists because operators kept asking background questions the playbook deliberately leaves
out: who funds it, who built it, how popular is it, and — most importantly — **how much should I trust
its predictions?** The honest answers shape how you read every report the engine produces.

Evidence labels follow `references/evidence-taxonomy.md`. Where a claim is press-only or single-source,
it is marked `unresolved` (reported) and worded conditionally. Numbers move fast; phrasing is cautious
on purpose.

## What MiroFish Is, And What It Is Built From

MiroFish turns an uploaded document into a parallel social world, runs many LLM agents inside it, and
writes a prediction-style report. Its own framing is "rehearse the future in a digital sandbox."

- The engine is best understood as an **orchestration layer on top of existing parts**, not a new
  simulation core. Chinese technical reviews summarized it as "assembly, not manufacturing"
  (组装而非制造): the social simulator is **OASIS** (camel-ai), persistent agent memory is **Zep**, and
  the document-to-graph step is **GraphRAG**. `doc-confirmed` (upstream README credits OASIS) /
  `analogy-based` for the reviewers' framing.
- Lineage: **BettaFish → MiroFish**. BettaFish (微舆) was the author's earlier public-opinion-analysis
  tool; MiroFish reuses that lineage (one of the official demos is seeded from a BettaFish report). A
  later project, **MindSpider**, is archived. `doc-confirmed` (BettaFish demo) / `unresolved` (reported)
  for the MindSpider lineage detail.
- The genuine novelty is **document-grounded *automatic* world construction**: most comparable systems
  need hand-written agent bios (Stanford), pre-built urban data (AgentSociety), or a fixed platform
  (OASIS). MiroFish builds the world from an arbitrary uploaded document. The engine, memory layer, and
  base model underneath are all borrowed. `doc-confirmed` / `unresolved` (reported) for the novelty claim.

## Backing And Origin

- **Strategic backing from Shanda Group (盛大集团)** is stated in the upstream README. `doc-confirmed`.
- Press widely reports the incubation deal was driven by Shanda's founder **Chen Tianqiao (陈天桥)**, and
  that he committed **~30M RMB (~$4.1M)** after seeing a rough demo, reportedly deciding within ~24 hours.
  The README does not state the amount; treat the figure and the speed as `unresolved` (reported, though
  corroborated across multiple outlets). Equity/structure undisclosed.
- The founder is reported to be a young (≈20) university senior — handle **`666ghj`**, name reported as
  **Guo Hangjiang (郭航江)** — who went from intern to project lead very quickly. His university is reported
  as **BUPT** in most sources but **USTC** in some reposts, so state it as "reportedly a BUPT senior,"
  not as settled fact. `unresolved` (reported).

## Adoption

GitHub popularity is best read as a **trajectory, not a single number**. Reported curve: created
late Nov 2025 → ~5.7k stars early Mar 2026 → ~14k mid-Mar → ~40k Apr → ~51k May → ~65k by Jun 2026, with
the repo repeatedly topping GitHub global trending. Safe wording for the guide: "tens of thousands of
stars and climbing." `unresolved` (reported); do not hardcode a precise count anywhere else in the guide.

## Release Timeline

- Tagged releases: **v0.1.0 = Dec 2025, v0.1.1 = Jan 2026, v0.1.2 = Mar 2026.** The first public release
  was **December 2025**; "March 2026" was the **viral breakout**, not the launch. `doc-confirmed`
  (release tags).
- No tagged release after v0.1.2 as of this snapshot; evolution since has been untagged main-branch
  maintenance plus a large community-PR backlog. `doc-confirmed`.
- The biggest April change was **internationalization**: English became the default `README.md` and the
  Chinese version moved to `README-ZH.md`; hard-coded Chinese UI/backend strings were replaced. This is
  why the upstream README now reads English-first. `doc-confirmed`.

## The Honest Epistemic Spine (read this before trusting any report)

This is the part that matters most for an operator. The short version: **MiroFish generates a plausible
narrative, not a validated prediction — and its makers say so.**

- **No published accuracy benchmarks.** There is no upstream backtest, calibration, Brier/log-loss, or
  reproducibility study against real-world outcomes. Independent commentators converge on this same
  point. `doc-confirmed` (by absence) / `unresolved` (reported, external critics).
- **The team's own stance**, quoted: "不追求绝对的预测准确率" — *not pursuing absolute prediction accuracy* —
  framed as letting the future "rehearse" in a sandbox. Take "prediction" with that caveat attached.
  `doc-confirmed` (maker statement, press).
- **Inherited OASIS herd bias.** The underlying simulator's own findings note that LLM agents "are more
  susceptible to herd behavior than humans" and polarization can be "even more pronounced." So apparent
  "emergence" is biased toward exaggerated consensus and extremity, not toward real-world distributions.
  `analogy-based` / `doc-confirmed` (OASIS paper).
- **One concrete divergence anchor:** an independent Strait-of-Hormuz experiment (≈200 agents, 7 sim-days)
  produced ~**47.9%** probability of shipping normalizing versus a Polymarket market price of ~**31%** — a
  ~17-point gap, with agents drifting toward "moderate/cooperative" self-censorship. Useful as a reminder
  that it models *public opinion*, not private information. `unresolved` (reported, single experiment).
- **Trading: used ≠ validated.** People do wire MiroFish into market workflows, but the best-documented
  run made only ~**$4,266 over 338 trades** before failing on private-information and very-short-horizon
  markets. Viral "millions in profit" stories are anonymous and unverified. Best at *qualitative/narrative*
  forecasting (opinion, reactions), weak at hard numeric targets. `unresolved` (reported).

Operator takeaway: score runs with `references/evaluation-rubric.md` for **run health and qualitative
usefulness**, and never present a MiroFish report as a calibrated probability of a real-world outcome.

## Comparative Landscape

Useful when someone asks "is this state of the art?" — it is impressive engineering, but it has not met
the validation bar that some peers have.

- **AgentSociety (Tsinghua, 2025)** — large-scale (10k+ agents, millions of interactions) and, crucially,
  **validated its outputs against real-world experiments** (polarization, information spread, UBI,
  hurricane response). This is the rigor bar MiroFish has **not** met. The cleanest contrast. `doc-confirmed`.
- **Stanford Generative Agents (2023)** — 25 agents in a sandbox town; goal was *believability* of daily
  life, not forecasting. `doc-confirmed`.
- **Stanford 1,000-person sim (2025)** — interview-grounded agents replicated human survey answers at
  ~**85%** of human self-consistency: a real benchmark MiroFish has no equivalent for. `doc-confirmed`.
- **OASIS (camel-ai)** — the engine underneath; scales to very large populations (capacity cited up to
  ~1M users) and provides the action set MiroFish uses. `doc-confirmed`.
- **a16z AI Town** — a JS/TS world-building starter kit; MiroFish is an analyst-facing forecasting shell
  by comparison. `doc-confirmed`.

## A Memorable Demo (reported)

The "Dream of the Red Chamber" (红楼梦) lost-ending simulation is the engine's most cited showcase: seeded
from the first 80 chapters, it reportedly built a graph of ~**905 entity nodes / ~3,822 edges**, ran
~**580 agent personas** over ~**30 rounds** (~2,000 interactions), and reproduced scholarly-consensus plot
outcomes — reportedly for a total backend cost of ~**14 RMB (~$2)**. Vivid, but `unresolved` (reported);
the exact triple of numbers could not be re-confirmed from a single primary source.

## Rumors — Do NOT Assert These As Fact

These circulate widely and are wrong, unverifiable, or misattributed. Keep them out of the guide and out
of any report you publish. All `unresolved`.

- **"1,000,000 agents."** That is **OASIS capacity**, not a MiroFish run. MiroFish's own README says
  "thousands"; real runs are hundreds to low thousands.
- **"92% accuracy"** (or any headline accuracy percentage) — no primary source exists.
- **Polymarket "millions in profit"** — anonymous social-media claims, no auditable results.
- **A standalone "OpenZep" repo** with specific coverage numbers — an issue *proposing* a local
  Zep-replacement exists, but the standalone repo and its "≈20% coverage / 168×161 rounds" specifics
  are unverified. Mention the *idea* of local memory replacement (see `model-proxy-guidance.md`), not
  those numbers.

## Where The Operational Detail Lives

For the things you can actually act on — the cloud-dependency forks, the issue/PR catalog, the Zep
rate-limit fixes, and the report-fabrication failure modes — see:

- `references/model-proxy-guidance.md` (routes, local-deployment forks)
- `references/graph-build-runbook.md` (Zep ingestion, ontology failures)
- `references/report-audit.md` (report fabrication failure modes)
- `references/debugging.md` (cross-stage symptoms)
