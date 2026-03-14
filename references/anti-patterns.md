# MiroFish Anti-Patterns

Use this file when you want to avoid the mistakes that waste budget, create misleading outputs, or make the guide less trustworthy.

## 1. Starting With The Biggest Run

Problem:

- large runs multiply every weakness in the seed, route, and runtime setup.

Fix:

- start with a pilot;
- scale only after artifacts look real.

## 2. Treating The Report As Ground Truth

Problem:

- the report is an LLM-generated summary layer, not the primary evidence layer.

Fix:

- verify important claims against `actions.jsonl`, platform databases, and `agent_log.jsonl`.

## 3. Fixing The Report Prompt Before The Seed

Problem:

- weak source material produces weak entities, weak personas, and weak reports.

Fix:

- improve source material and simulation requirements before touching report-stage prompts.

## 4. Using One Seed Document For Multiple Scenarios

Problem:

- mixed contexts create muddled graphs and generic personas.

Fix:

- split unrelated questions into separate source packages.

## 5. Omitting Dates And Temporal Order

Problem:

- the graph and agent memory layers work better when facts are anchored in time.

Fix:

- state what happened, when it happened, and what changed afterward.

## 6. Ignoring Per-Platform Artifacts

Problem:

- a final action count can hide the fact that one platform barely ran.

Fix:

- inspect `twitter/actions.jsonl`, `reddit/actions.jsonl`, and the matching databases separately.

## 7. Assuming More Rounds Means Better Reasoning

Problem:

- extra rounds can add cost without adding meaningful new behavior.

Fix:

- evaluate action diversity and evidence quality, not just round count.

## 8. Trusting A Proxy Route Because It Is Cheap

Problem:

- cheap routes can fail on structured JSON, tool-heavy report generation, or content-type quirks.

Fix:

- validate the full pipeline before trusting the route for serious runs.

## 9. Committing Raw Logs Or Private Source Material

Problem:

- this breaks repository hygiene and can leak sensitive data.

Fix:

- keep local research dumps ignored;
- redact examples and logs before publishing them.

## 10. Promoting Analogies To Facts

Problem:

- adjacent-system lessons are useful, but they are not direct evidence about MiroFish behavior.

Fix:

- label analogy-based guidance clearly and keep code-confirmed claims separate.

## 11. Diagnosing Only From The UI

Problem:

- the UI can lag behind backend state or hide useful error context.

Fix:

- trust files and backend logs before you trust the visual status chip.

## 12. Changing Too Many Variables At Once

Problem:

- if source material, model, rounds, and requirements all change together, you learn nothing.

Fix:

- change one major variable per comparison and record it explicitly.
