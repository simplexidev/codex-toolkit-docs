# Model routing and context cost

The product's `config/model-routing.json` is advice, not an automatic model router. It
describes cheap, coding, difficult, and exceptional tiers. Actual native-agent models are
set in TOML and remain subject to account availability; remove explicit model settings
to inherit the parent session when appropriate.

Good routing starts before model choice: search before reading, compute repository facts
with AgentTool, keep full artifacts on disk, and open only the bounded evidence needed.
Use JEV only for a small uncertain classification. Escalate to stronger Codex reasoning
for hard debugging or design, not routine mechanical work.

Evaluation must measure correctness alongside tokens, turns, tool calls, elapsed time,
and file reads. A cheaper answer that misses a defect is a regression. Evaluation budgets
are comparison thresholds, not live task-abort limits. See
[context and token efficiency](context-and-token-efficiency.md) and the
[evaluation methodology](../metrics/methodology.md).
