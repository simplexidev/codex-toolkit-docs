# Documentation map

These pages describe the toolkit's `develop/v3.0.0` development line. Runtime files and
release artifacts remain canonical in the product repository.

## Get started

- [Overview and prerequisites](getting-started/index.md)
- [Install and verify](getting-started/install.md)
- [Update](getting-started/update.md)
- [Uninstall](getting-started/uninstall.md)

## Use and configure

- [Common workflows](guides/usage.md)
- [Configuration](guides/configuration.md)
- [Project integration](guides/project-integration.md)
- [AgentTool command reference](reference/agenttool.md)
- [Skills catalog](reference/skills.md)
- [Native agents](reference/agents.md)
- [Releases and versioning](reference/releases-and-versioning.md)

## Understand the system

- [How the pieces work together](concepts/index.md)
- [JEV and bounded judgment](concepts/jev.md)
- [Model routing and context cost](concepts/model-routing.md)
- [Context and token efficiency](concepts/context-and-token-efficiency.md)
- [Architecture](architecture/index.md)
- [Runtime data flows](architecture/runtime-data-flows.md)
- [Upstream integrations](architecture/upstream-integrations.md)
- [Security and privacy](security/index.md)
- [JEV credentials and subprocesses](security/jev-credentials-and-subprocesses.md)
- [Third-party integrations and notices](security/third-party-and-notices.md)
- [Metrics and evaluation](metrics/index.md)
- [Evaluation methodology](metrics/methodology.md)
- [Interpret the metrics dashboard](metrics/dashboard.md)

The metrics dashboard and sanitized versioned data will be published at
<https://simplexidev.github.io/sdeveng-metrics-dashboard/>; during this migration they remain
at <https://simplexidev.github.io/codex-toolkit-metrics/>. This repository explains how to
interpret them; it does not implement or host the evaluator.

## Solve problems and contribute

- [Troubleshooting](troubleshooting/index.md)
- [Product development](development/index.md)
- [Three-repository development workflow](development/workflow.md)
- [Skill authoring](development/skill-authoring.md)
- [Release process](development/releases.md)
- [Contributing](contributing/index.md)
- [Examples](examples/index.md)

## Migration control

- [Source audience and migration manifest](migration-manifest.md)

Runtime links should target canonical files in `simplexidev/sdeveng`; until the repository
rename phase, those links use the legacy `simplexidev/codex-toolkit` URL. Human pages
may quote small, stable examples, but they must not become a required runtime input.
