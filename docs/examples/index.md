# Examples

## Inspect and validate a change

```console
dotnet /path/to/codex-toolkit/tools/AgentTool.cs repo changed-files \
  --root /path/to/project --base main
dotnet /path/to/codex-toolkit/tools/AgentTool.cs repo affected-projects \
  --root /path/to/project --base main
dotnet /path/to/codex-toolkit/tools/AgentTool.cs -- dotnet verify \
  --root /path/to/project --project tests/App.Tests.csproj
```

This keeps discovery deterministic and validation targeted. If shared inputs make the
dependency graph uncertain, the toolkit widens validation.

## Summarize a large artifact

```console
dotnet /path/to/codex-toolkit/tools/AgentTool.cs logs summarize \
  --root /path/to/project --file build.log
```

Share the bounded summary and a reviewed local path, not an unfiltered log that may
contain source, environment values, or credentials.

## Screen sanitized candidates with JEV

```json
{
  "capability": "relevance",
  "purpose": "docs-impact",
  "deterministicNarrowed": true,
  "query": "Which excerpts describe build configuration?",
  "candidates": [
    {"id": "readme", "text": "Build with the .NET 10 SDK."},
    {"id": "license", "text": "Released under the MIT License."}
  ]
}
```

```console
dotnet /path/to/codex-toolkit/tools/AgentTool.cs jev screen \
  --input candidates.json --dry-run
```

Review the exact payload before adding `--safe-input` for a live request. Open all
`INCLUDE` and `REVIEW` candidates; never use JEV to make a security authorization.
