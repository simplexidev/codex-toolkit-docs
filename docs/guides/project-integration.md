# Add the toolkit to a project

Install the central toolkit once, then copy only the relevant files from the product's
[`templates/project`](https://github.com/simplexidev/sdeveng/tree/develop/v3.0.0/templates/project)
directory into a trusted target repository.

1. Merge the template `AGENTS.md` with existing instructions and fill in architecture,
   validation targets, paths, and deployment constraints.
2. Merge `.codex/config.toml`; do not replace established project settings.
3. Review optional `.NET` defaults individually: `.editorconfig`, `Directory.Build.props`,
   `Directory.Packages.props`, `global.json`, and `version.json`. They are starting points,
   not required product dependencies.
4. Merge the pull-request template with the repository's existing review policy.
5. Run the project's normal checks and review the resulting diff.

The `version.json` template is a Nerdbank.GitVersioning starting point; the toolkit does
not install that tool. Central package management templates add no forced packages.
Framework and SDK choices must match the target project.

You can inspect a target from anywhere:

```console
dotnet /path/to/sdeveng/tools/AgentTool.cs repo affected-projects --root /path/to/project
```

MSBuild evaluation can execute imported project logic, so use it only on trusted
repositories. Shared or unrecognized inputs deliberately widen validation rather than
hiding possible dependents.
