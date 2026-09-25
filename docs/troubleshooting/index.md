# Troubleshooting

Start with:

```console
dotnet tools/AgentTool.cs doctor
dotnet tools/AgentTool.cs help
```

`doctor` checks required .NET/Git prerequisites and reports optional Codex, GitHub CLI,
tool, installation, and JEV status without printing a credential.

## Command options disappear

The `dotnet` host may consume options such as `--help` and `--project`. Insert `--`:

```console
dotnet tools/AgentTool.cs -- dotnet verify --project /path/to/App.csproj
```

## Toolkit root not found

Run the source file from its checkout, pass `--toolkit /path/to/sdeveng`, or set
the non-secret `SDEVENG_ROOT` variable. `CODEX_TOOLKIT_ROOT` remains a supported legacy
alias for v2 installations.

## Install reports a conflict

The installer never force-overwrites. Preserve the destination, inspect its owner and
target, then relocate it yourself only if replacement is intended. Use the same `--home`
and `--codex-home` values across install, update, and uninstall.

If the checkout moved, move it back and uninstall before relocating it. On Windows,
enable Developer Mode or suitable symlink permission; `--bin` remains unsupported.

## Skills appear twice

Do not install skills both through the local plugin marketplace and AgentTool's direct
skill links. Keep the discovery method you prefer; the global instructions and native
agent still require AgentTool if wanted.

## Affected-project analysis fails

MSBuild evaluation is not treated as an empty dependency graph. Check the selected SDK,
project imports, permissions, and trustworthiness of imported logic. Shared or unknown
inputs may intentionally broaden the validation set.

## JEV returns `REVIEW`

Check `JEV_MODE`, credential availability, endpoint, timeout, payload size and shape, and
the configured thresholds. Do not print the key or raw provider body. Uncertainty is an
expected result, not a reason to force inclusion or exclusion. Required-mode service
failure exits with status 3.

## .NET cannot write its cache

In a restricted sandbox, point `DOTNET_CLI_HOME` and `XDG_DATA_HOME` at writable temporary
directories. Restore, package audit, and some tests may require network access.

## A diagnostic plan cannot narrow the work

`repo affected-projects`, `dotnet inspect`, build plans, and test plans use MSBuild
evaluation. An import error, unavailable SDK, or untrusted imported project logic is a
real boundary: correct the environment or use a trusted repository before treating the
graph as complete. Do not turn an evaluation failure into an empty affected-project list.

## GitHub commands fail

Install and authenticate the GitHub CLI independently, then verify its access in the
target repository. `github actions`, PR status, review comments, and issue-start need
network access and repository permission; AgentTool deliberately does not supply either.
