# Contributing

Choose the repository by ownership before editing:

- Runtime behavior, plugin skills, AgentTool, agent definitions, templates, schemas, and
  releases: [`sdeveng`](https://github.com/simplexidev/sdeveng).
- Human guides and explanations: this repository.
- Evaluator, scenarios, metrics schema/data, and dashboard:
  [`sdeveng-metrics-tooling`](https://github.com/simplexidev/sdeveng-metrics-tooling).

Read the target repository's `AGENTS.md`, start from its designated base, and keep one
change focused on one concern. `AGENTS.md` guides coding agents; these documentation pages
guide people, so do not duplicate agent instructions wholesale. Preserve unrelated work.
Never commit secrets, private source, raw prompts/results, absolute developer paths, or
temporary planning notes. Follow the [five-repository development workflow](../development/workflow.md)
for branch/PR discipline, validation, publication, and release expectations.

For documentation changes, verify every behavioral claim against product code, schemas,
tests, or the selected release. Write for people instead of copying agent instructions.
Use stable GitHub links for cross-repository ownership and relative links within this
site. Run a Markdown link check, formatting checks, and review rendered pages before
requesting review.

Product changes should include focused automated tests and relevant eval scenarios.
Metrics changes must retain keyless normal CI and publish only schema-valid sanitized
aggregates. Pull requests should explain scope, validation, security/privacy impact, and
any deferred or on-demand gate.

See [product development](../development/index.md), [skill authoring](../development/skill-authoring.md),
and [security](../security/index.md).
