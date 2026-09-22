# Documentation map

This is the planned human navigation for the v2 documentation set. Target pages may be
added in later migration phases; the map fixes ownership and destinations before prose
is moved or rewritten.

## Get started

- `getting-started/index.md` — prerequisites, mental model, and first successful run
- `getting-started/install.md` — install and verify
- `getting-started/update.md` — update an owned installation safely
- `getting-started/uninstall.md` — remove toolkit-owned links and state

## Use and configure

- `guides/usage.md` — common workflows and bounded output
- `guides/configuration.md` — configuration files, precedence, and examples
- `guides/project-integration.md` — adopt the project template without overwriting policy
- `reference/agenttool.md` — AgentTool commands and output contracts
- `reference/skills.md` — human catalog of skill triggers and limitations
- `reference/agents.md` — custom-agent roles, permissions, and evidence expectations
- `reference/releases-and-versioning.md` — supported lines, changelog, and release semantics

## Understand the system

- `concepts/index.md` — deterministic tooling, bounded judgment, and GPT reasoning
- `concepts/jev.md` — human explanation of JEV, routing, uncertainty, and calibration
- `architecture/index.md` — repository boundaries, components, and data flow
- `security/index.md` — security, credentials, privacy, and artifact handling
- `metrics/index.md` — evaluation methodology and the metrics-site relationship

The metrics dashboard and sanitized versioned data will be published at
<https://simplexidev.github.io/codex-toolkit-metrics/>. This repository explains how to
interpret them; it does not implement or host the evaluator.

## Solve problems and contribute

- `troubleshooting/index.md` — installation, configuration, command, and JEV failures
- `development/index.md` — local product development and validation
- `contributing/index.md` — contribution flow, documentation standards, and review
- `examples/index.md` — end-to-end, sanitized examples

## Migration control

- [Source audience and migration manifest](migration-manifest.md)

Runtime links should target canonical files in `simplexidev/codex-toolkit`. Human pages
may quote small, stable examples, but they must not become a required runtime input.
