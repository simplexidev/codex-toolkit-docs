# Author a skill

Create a skill only for a distinct, recurring workflow with a precise trigger. Keep its
`SKILL.md` focused on non-obvious decisions and load detailed references lazily. Add
`agents/openai.yaml` metadata; disable implicit invocation for expensive, mutating, or
security-sensitive workflows.

Every skill needs a realistic positive scenario, a negative trigger, and a safety
invariant under product `evals/`. Deterministic support belongs in AgentTool with unit
tests. Validate actual YAML, TOML, JSON, and schemas with standard parsers and an official
skill validator when available.

An offline scenario proves structural consistency, not behavioral quality. Measured
forward runs belong in the metrics repository and must compare correctness as well as
cost. Do not copy upstream skills; reference and install them separately.

When behavior affects people, update these human docs independently. Do not replace a
runtime `SKILL.md` or compact agent reference with a link into this repository.
