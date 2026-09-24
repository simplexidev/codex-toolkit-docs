# How the toolkit works

The toolkit uses an intelligence hierarchy:

1. **AgentTool and structured tooling** compute exact, reproducible facts and keep raw
   output off the conversation when possible.
2. **JEV** answers small semantic questions with explicit thresholds and a `REVIEW`
   outcome for uncertainty.
3. **Codex** handles implementation, synthesis, debugging, and every result that cannot
   safely be reduced to the first two layers.
4. Stronger reasoning is reserved for cases whose difficulty justifies its cost.

The plugin is the discovery container for skills. A skill tells Codex when and how to
apply a narrow workflow. Skills call AgentTool where deterministic support exists and
load compact runtime references only when needed. The native reviewer agent is separate
from the plugin because it is discovered from Codex's agent directory. The project
template adds repository-specific constraints without duplicating the central toolkit.

This separation matters: broad capability does not require loading every instruction,
tool, or reference into every conversation. See [architecture](../architecture/index.md),
[runtime data flows](../architecture/runtime-data-flows.md),
[context and token efficiency](context-and-token-efficiency.md),
[skills](../reference/skills.md), [agents](../reference/agents.md), and [JEV](jev.md).
