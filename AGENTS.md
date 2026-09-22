# Human documentation development

This repository owns human-oriented documentation only. Do not add executable runtime
logic, Codex skills, agent instructions, compact agent references, evaluation runners,
dashboard code, or metrics datasets.

Before migrating product documentation, search `simplexidev/codex-toolkit` consumers.
Agent- or runtime-consumed material stays in the product repository; write a separate
human explanation here when useful. In particular, never replace the compact JEV
references loaded by the runtime skill with links into this repository.

Keep navigation, examples, and cross-repository ownership clear. Prefer task-oriented
guides, verified commands, and links to canonical runtime schemas or release artifacts.
Mark version-specific behavior. Do not publish secrets, private source, raw prompts or
results, local absolute paths, or unsanitized logs. Human metrics documentation may
explain methods and link to the metrics site, but implementation and data stay in
`simplexidev/codex-toolkit-metrics`.

For changes, check links and formatting, review the rendered Markdown, and preserve
unrelated work. Update `docs/migration-manifest.md` when source ownership or consumers
change.
