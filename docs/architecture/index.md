# Architecture

SimplexiDev Engineering Toolkit is deliberately one runtime product rather than a collection of bundled
plugins. It has one discoverable plugin, one opt-in project-template bundle, one
deterministic utility, and a small set of separately discovered native agents. This keeps
installation ownership and routing understandable while allowing each workflow to load
only the material it needs.

## One plugin and one template

The unified plugin lives in `sdeveng` at
[`plugins/sdeveng/`](https://github.com/simplexidev/codex-toolkit/tree/develop/v3.0.0/plugins/sdeveng)
(currently served from the legacy repository URL).
Its manifest provides discovery metadata, `skills/` contains narrow task workflows, and
`references/` contains compact runtime material loaded only when a workflow calls for it.
Adding a capability normally means extending this plugin; it does not mean creating
another toolkit plugin or installing an upstream marketplace wholesale.

The single template bundle lives in `sdeveng` at
[`templates/project/`](https://github.com/simplexidev/codex-toolkit/tree/develop/v3.0.0/templates/project)
(currently served from the legacy repository URL).
It is source material for adopting repositories: project instructions, Codex settings,
pull-request conventions, and optional .NET defaults. Copying selected template files
does not make the adopting repository depend on the toolkit checkout, this documentation,
or the metrics site. Template placeholders and policy choices must be reviewed for the
target project rather than copied blindly.

These two boundaries solve different problems. The plugin is centrally installed runtime
behavior; the template is an explicit, reviewable project customization. Human docs are
neither and are never loaded by the runtime.

## Intelligence hierarchy

The preferred order is a cost and authority hierarchy, not a requirement that every task
use every layer:

1. **AgentTool and structured tooling** establish exact facts, validate schemas, select
   affected projects, compact artifacts, and run bounded commands. If the question can be
   computed, its result should not depend on a semantic guess.
2. **A narrowly triggered skill** supplies the workflow: when to inspect, which exact tool
   to call, what safety checks apply, and which compact reference may be loaded.
3. **JEV** may classify a small, sanitized, deterministically narrowed ambiguity. It is
   optional and cannot authorize actions or decide architecture.
4. **Codex/GPT reasoning** interprets evidence, debugs, designs, writes, and handles JEV's
   `REVIEW` path. Stronger reasoning is reserved for genuinely difficult work.
5. **A custom agent** is used only when an independent context or specialist boundary has
   demonstrated value. It is not a default way to split routine work.

The skill is shown before AgentTool in request routing but does not outrank exact evidence:
it tells Codex when and how to obtain that evidence. Likewise, an agent can use skills and
AgentTool, but its role description does not override their safety constraints.

```text
request + installed/project instructions
  -> narrow skill or direct deterministic command
     -> exact facts and bounded local artifacts
     -> optional JEV classification of residual ambiguity
  -> Codex interpretation or implementation
  -> optional evidence-backed independent agent
  -> validation and concise result
```

## Product components

Production executable logic lives in the product repository's single .NET 10 file-based
app, [`tools/AgentTool.cs`](https://github.com/simplexidev/codex-toolkit/blob/develop/v3.0.0/tools/AgentTool.cs)
in `sdeveng` (currently served from the legacy repository URL).
It owns CLI parsing, bounded process execution, repository and MSBuild inspection, output
compaction, installation ownership, result-store operations, and JEV HTTP requests. The
utility uses the .NET base class library; tests link the same source rather than maintaining
a second implementation.

`global/AGENTS.md` supplies broad installed policy. Native-agent TOML files under `agents/`
are discovered separately, because plugin registration does not populate Codex's native
agent directory. `config/` and `schemas/` define machine-checked policy and inputs.
Agent-consumed references stay inside the product repository, including the compact JEV
and v2 baseline references.

Installing through a local plugin marketplace discovers plugin skills but does not install
global instructions or native agents. AgentTool's lifecycle commands can instead link the
owned instructions, agents, and skills. Use one skill-discovery route so a skill is not
presented twice.

## Repository boundaries

- `sdeveng` (currently served from the legacy
  [`codex-toolkit`](https://github.com/simplexidev/codex-toolkit) URL) owns runtime code,
  configuration, schemas, tests, installation, agent-consumed references, and releases.
- `sdeveng-docs` (currently served from the legacy
  [`codex-toolkit-docs`](https://github.com/simplexidev/codex-toolkit-docs) URL) owns human
  explanations. It is not a runtime dependency.
- `sdeveng-metrics-tooling` (currently served from the legacy
  [`codex-toolkit-metrics`](https://github.com/simplexidev/codex-toolkit-metrics) URL) owns the
  evaluator, scenarios, schemas and statistics, sanitized data, dashboard, and Pages.

The product works without either sibling checkout. Metrics evaluation needs a subject
checkout when it measures the product, but the product never calls into the evaluator.

Continue with [runtime data flows](runtime-data-flows.md),
[context and token efficiency](../concepts/context-and-token-efficiency.md), and
[upstream derivation](upstream-integrations.md).
