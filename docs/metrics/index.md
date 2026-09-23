# Metrics and evaluation

Evaluation implementation, scenarios, statistics, sanitized history, and dashboard code
belong to
[`simplexidev/codex-toolkit-metrics`](https://github.com/simplexidev/codex-toolkit-metrics).
The intended Pages location is <https://simplexidev.github.io/codex-toolkit-metrics/>;
until Pages is enabled, use the repository as the source of truth.

The product's `AgentTool eval` command performs inexpensive offline integrity checks for
skill scenarios and fixtures. Unit tests cover executable behavior. Neither by itself
proves that a skill improves agent quality or reduces tokens.

Meaningful comparisons run the same scenario, repository revision, prompt, and OpenAI/GPT
model with and without the skill. They record correctness first, then tokens, turns, tool
calls, elapsed time, file reads, routing behavior, static context cost, and unnecessary
broad operations. Provider usage should be measured rather than estimated. A result is a
regression if it saves cost by missing required behavior or violating a safety invariant.

Normal CI is keyless and synthetic or mocked. Raw prompts, responses, transcripts,
private source, and logs remain in ignored local storage or short-lived CI artifacts.
Only reviewed aggregates accepted by the metrics repository's versioned public schema
may be committed or published. Evaluation executors and judges use OpenAI/GPT models;
JEV can support bounded classification but does not replace the evaluator or judge.
