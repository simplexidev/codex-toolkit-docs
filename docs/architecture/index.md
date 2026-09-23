# Architecture

Production executable logic lives in the product repository's single .NET 10 file-based
app, [`tools/AgentTool.cs`](https://github.com/simplexidev/codex-toolkit/blob/develop/v2.0.0/tools/AgentTool.cs).
It owns CLI parsing, bounded process execution, repository and MSBuild inspection, output
compaction, installation ownership, result-store operations, and HTTP judgments. The
utility uses the .NET base class library; tests link the same source rather than a second
implementation.

## Components and flow

```text
user request
  -> global + project instructions
  -> narrowly matched plugin skill
  -> AgentTool for exact facts
  -> optional JEV for bounded uncertainty
  -> Codex for reasoning and implementation
  -> concise result + paths to local evidence
```

The plugin contains skills and compact runtime references. Native agents are installed
separately because plugin installation does not populate Codex's native agent directory.
The project template is copied selectively into target repositories. Upstream .NET tools
and skills are referenced, never vendored or automatically installed.

## Repository boundaries

- [`codex-toolkit`](https://github.com/simplexidev/codex-toolkit): runtime product,
  schemas, tests, installer, and releases.
- [`codex-toolkit-docs`](https://github.com/simplexidev/codex-toolkit-docs): human prose;
  never a runtime dependency.
- [`codex-toolkit-metrics`](https://github.com/simplexidev/codex-toolkit-metrics):
  evaluator, scenarios, sanitized data, and dashboard.

Agent/runtime references stay product-local. The product may be used without either
sibling checkout.
