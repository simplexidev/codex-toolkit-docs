# Start here

Codex Toolkit is a collection of focused Codex workflows for repository and .NET work.
It combines one local command-line program, a Codex plugin containing 24 skills, a
project template, global instructions, and one optional read-only reviewer agent.

The toolkit exists to make routine work cheaper and more predictable. AgentTool computes
facts such as changed files, affected projects, Git state, health checks, and compact log
summaries. JEV can make a narrowly defined semantic classification when exact tooling is
not enough. Codex remains responsible for open-ended analysis, implementation, and any
uncertain result.

## Prerequisites

- Git.
- The .NET 10 SDK selected by the product's `global.json`.
- A stable checkout of the
  [`codex-toolkit` repository](https://github.com/simplexidev/codex-toolkit).
- Codex, if you want installed instructions, skills, or the native reviewer agent.
- Optional: GitHub CLI for GitHub-aware commands and a TypeSafe API credential for live
  JEV calls. Neither is needed for normal tests or offline validation.

## First successful run

From the toolkit checkout:

```console
dotnet tools/AgentTool.cs install --dry-run
dotnet tools/AgentTool.cs install --bin
dotnet tools/AgentTool.cs doctor
dotnet tools/AgentTool.cs repo changed-files --root /path/to/project
```

Use `dotnet tools/AgentTool.cs ...` instead of the installed launcher on Windows or if
`~/.local/bin` is not on `PATH`. AgentTool emits bounded structured JSON; detailed command
output is kept in the target repository's ignored `.agent-tool/` directory when needed.

Next: [installation details](install.md), [common workflows](../guides/usage.md), and
[what installation changes](../architecture/index.md).
