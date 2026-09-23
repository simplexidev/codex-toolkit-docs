# Native agents

The current development baseline includes one native agent: `reviewer`. It is a bounded,
read-only independent reviewer for explicitly requested reviews or substantial,
high-risk completed diffs. It prioritizes correctness, regressions, security, concurrency,
resource lifetimes, compatibility, and missing tests, with concrete evidence rather than
style-only feedback.

The agent cannot change files or merge. Its configured model is a product default subject
to account availability; edit the installed TOML or remove model fields to inherit the
parent session if needed.

Native agents live under product `agents/` and are linked into the Codex agent directory
by AgentTool. They are separate from plugin skills and from `AGENTS.md` instructions:
skills guide a task, agents provide a bounded delegated role, and instruction files set
repository policy.
