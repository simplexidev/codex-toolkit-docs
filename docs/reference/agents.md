# Native agents

The current development baseline includes one native agent: `reviewer`. It is a bounded,
read-only independent reviewer for explicitly requested reviews or substantial,
high-risk completed diffs. It prioritizes correctness, regressions, security, concurrency,
resource lifetimes, compatibility, and missing tests, with concrete evidence rather than
style-only feedback.

The agent cannot change files, merge, delegate, or request further reviews. The current
product TOML sets `gpt-5.6-terra` with high reasoning and a read-only sandbox; availability
is account-dependent. Edit the installed TOML—or remove model fields—to inherit the parent
session if needed. It should report supported file/line findings or an explicit no-findings
result, not style-only feedback.

Native agents live under product `agents/` and are linked into the Codex agent directory
by AgentTool. They are separate from plugin skills and from `AGENTS.md` instructions:
skills guide a task, agents provide a bounded delegated role, and instruction files set
repository policy.
