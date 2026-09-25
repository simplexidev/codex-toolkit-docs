# Install

Keep the toolkit checkout at a stable path. The installer creates symbolic links; it
does not copy the runtime or rewrite your existing Codex configuration.

```console
git clone https://github.com/simplexidev/codex-toolkit.git sdeveng
cd sdeveng
dotnet tools/AgentTool.cs install --dry-run
dotnet tools/AgentTool.cs install --bin
dotnet tools/AgentTool.cs doctor
```

Review the dry-run before installing. Conflicts stop the operation instead of
overwriting files. Repeating installation is safe when the recorded targets still match.

## What changes

The default install creates links for:

- `global/AGENTS.md` at the selected Codex home's `AGENTS.md`;
- each product `agents/*.toml` file under the Codex home's `agents/` directory;
- each toolkit skill under the user's `.agents/skills/` directory; and
- on Unix with `--bin`, `~/.local/bin/sdeveng (legacy codex-agent-tool)`.

Ownership metadata is stored under the selected Codex directory so update and uninstall
can distinguish toolkit-owned links from user files. Existing `config.toml` is never
edited. Installation refuses symlinked state or destination parents.

`--home DIR` selects an isolated user profile for testing and ignores ambient
`CODEX_HOME`. `--codex-home DIR` changes only the Codex directory. Without `--home`, an
explicit `--codex-home` wins, then `CODEX_HOME`, then `~/.codex`.

## Platform notes

On Unix, add `~/.local/bin` to `PATH` if you use `--bin`. A ZIP extraction may require
`chmod +x tools/AgentTool.cs` for the launcher; direct `dotnet` invocation still works.

On Windows, `--bin` is unsupported. Invoke `dotnet C:\path\to\sdeveng\tools\AgentTool.cs`
and enable Developer Mode or otherwise grant symlink permission. Do not run as
administrator merely to bypass an ownership conflict.

## Plugin marketplace alternative

You may register the checkout as a local marketplace:

```console
codex plugin marketplace add /absolute/path/to/sdeveng
```

Choose either plugin-provided skills or direct skill links to avoid duplicate discovery.
The marketplace does not install the global instructions or native agent, so use
AgentTool for those components if desired.
