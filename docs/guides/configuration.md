# Configuration

Central configuration lives under the product repository's `config/` directory and is
validated by matching JSON Schemas under `schemas/`. Project files cannot silently
override this policy.

| File | Purpose |
|---|---|
| `toolkit.json` | Product version, optional tools, and descriptive integrations |
| `jev.json` | JEV mode, endpoint, model, timeout, limits, thresholds, and cache lifetime |
| `model-routing.json` | Advisory model tiers; not an automatic resolver |
| `output-limits.json` | Maximum summary lines, items, line length, and output characters |
| `repo-health.json` | Framework and MSBuild property policy |
| `ecosystem.json` | Repository ownership and product paths |

Treat the product's
[`schemas/`](https://github.com/simplexidev/codex-toolkit/tree/develop/v2.0.0/schemas)
as canonical for fields and allowed values. Keep configuration and schema changes in the
same product contribution.

## Location and precedence

AgentTool locates the toolkit from its source path. `--toolkit DIR` overrides that path,
followed by `CODEX_TOOLKIT_ROOT`. `--root DIR` selects the target repository.

For installation, `--home DIR` creates an isolated profile and ignores ambient
`CODEX_HOME`; `--codex-home DIR` is an explicit Codex directory. Existing user
`config.toml` is never edited. The example `config/codex-recommended.toml.example` must be
merged selectively by the user.

## JEV environment overrides

- `TYPESAFE_API_URL`: complete HTTPS endpoint.
- `JEV_MODEL`: provider model name.
- `JEV_MODE`: configured operating mode.
- `JEV_TIMEOUT_SECONDS`: positive timeout.
- `TYPESAFE_API_KEY`: the only secret input.

The API key is accepted only from AgentTool's environment, removed from every child
process, never accepted as a command-line option, and never persisted. See
[credentials and privacy](../security/index.md).
