# Skills catalog

The plugin contains 24 narrowly triggered skills. A skill supplies workflow guidance;
it does not grant new authority or make every named external tool available.

| Skill | Use it for |
|---|---|
| `address-pr-review` | Address concrete review comments |
| `agent-maintenance` | Maintain installed toolkit components or configuration |
| `api-compatibility` | Check a real public .NET API surface change |
| `architecture-change` | Plan or review a component-boundary change |
| `benchmark` | Create or run an explicitly requested benchmark |
| `dependency-change` | Change .NET package references safely |
| `diagnostics` | Collect or inspect counters, traces, dumps, or GC artifacts |
| `docs-impact` | Find documentation affected by a change |
| `dotnet-format` | Check or apply C# formatting |
| `dotnet-verify` | Validate affected .NET projects and tests |
| `finish-pr` | Prepare an authorized push and pull request |
| `issue-start` | Start a safe branch for a specific open issue |
| `jev-judgment` | Reduce a bounded ambiguous candidate set |
| `package-audit` | Audit .NET vulnerability metadata on request |
| `performance-investigation` | Investigate an observed performance regression |
| `prepare-commit` | Check local commit scope and Git safety |
| `release-verify` | Run explicitly requested full/release validation |
| `repo-health` | Compare repository configuration with toolkit policy |
| `reproducible-build` | Audit deterministic build reproducibility |
| `roadmap-next` | Choose from explicit roadmap/dependency metadata |
| `sbom` | Generate or verify a release SBOM on request |
| `security-scan` | Run or triage scoped analyzers and SARIF |
| `test-quality` | Assess targeted tests and optional mutation testing |
| `versioning` | Apply an existing Git-derived version policy |

Expensive, mutating, security-sensitive, or release-oriented skills are intentionally
on demand. `finish-pr` prepares publishing work but does not override approval or merge
policy. JEV and package-audit skills also require their explicit prerequisites. Runtime
instructions remain canonical in the
[`skills` directory](https://github.com/simplexidev/codex-toolkit/tree/develop/v2.0.0/plugins/codex-toolkit/skills);
they are not copied here as human prose.
