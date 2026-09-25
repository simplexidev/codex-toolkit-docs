# SimplexiDev Engineering Toolkit documentation

SimplexiDev Engineering Toolkit gives Codex a small set of safe, repeatable repository workflows backed by
one .NET utility. It favors exact computation first, bounded semantic judgment only when
useful, and general model reasoning for work that genuinely needs it.

This is the human documentation for
[`simplexidev/codex-toolkit`](https://github.com/simplexidev/codex-toolkit). Start with
[what the toolkit is](docs/getting-started/index.md), then [install it](docs/getting-started/install.md)
or browse the [documentation map](docs/README.md). The public metrics dashboard is at
<https://simplexidev.github.io/codex-toolkit-metrics/>; read the
[interpretation guide](docs/metrics/dashboard.md) before comparing results.

The repositories have deliberately separate jobs:

- [`codex-toolkit`](https://github.com/simplexidev/codex-toolkit) owns the plugin,
  project template, AgentTool, skills, native agent, runtime references, and releases.
- This repository owns human installation, usage, architecture, security, and
  contributor guidance. Nothing here is loaded at runtime.
- [`codex-toolkit-metrics`](https://github.com/simplexidev/codex-toolkit-metrics) owns
  evaluation code, scenarios, sanitized metrics, and the dashboard.

These pages describe the `develop/v3.0.0` development line unless a page says otherwise.
For an installed release, prefer the documentation and configuration shipped with that
tag when behavior differs.

## Contributing

Read the [contributor guide](docs/contributing/index.md). Repository automation also
uses `AGENTS.md`; it is policy for editing this repository, not product documentation.

## License

MIT. See [LICENSE](LICENSE).
