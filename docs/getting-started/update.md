# Update

AgentTool does not fetch, pull, reset, or select a release for you. Update the checkout
with your normal reviewed Git process, then reconcile installed links:

```console
git fetch --tags origin
# Select and review the desired tag or branch with your normal Git workflow.
dotnet tools/AgentTool.cs update --dry-run
dotnet tools/AgentTool.cs update
dotnet tools/AgentTool.cs doctor
```

`update` is ownership-aware and idempotent. It refreshes the planned link set and removes
recorded links for components that no longer exist in that checkout. A changed or
replaced destination is preserved and reported rather than overwritten.

Do not move an installed checkout. [Uninstall](uninstall.md), move it, and install again.
When using `--home` or `--codex-home`, pass the same values used for installation.
