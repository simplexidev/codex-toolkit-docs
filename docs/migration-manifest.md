# Source audience and migration manifest

## Scope and decision rules

This manifest audits the 67 tracked Markdown, text, and legal-document files in
`simplexidev/codex-toolkit` at commit `a79cbb9` on `develop/v2.0.0`. It records
consumers before any later migration. No product file was moved or deleted by this
bootstrap.

Audience values:

- **HUMAN** — intended for people; no agent or machine depends on its prose.
- **AGENT** — installed, loaded, or explicitly followed by Codex/skills.
- **DUAL-USE** — meaningful to people and also path-sensitive to an agent, template,
  release, or platform workflow.
- **INTERNAL-MACHINE** — generated evidence, test fixtures, or workflow control that is
  not part of the public human documentation set.

`Must remain` means the current file must remain in the product repository. A human
destination is a separate explanation or copy, never a new runtime dependency. `No`
means a later product phase may remove the source only after repairing product-local
links, validation, release packaging, and tests.

## Human and repository-level documents

| Product source | Audience | Skill references | Agent references | Runtime/path sensitivity | Human migration or copy | Must remain | Proposed human destination |
|---|---|---|---|---|---|---|---|
| `README.md` | HUMAN | None | None | Explicitly included in release archives; links to product `docs/` and templates | Rewrite as the docs landing/get-started content; retain a concise product landing while releases need it | Yes | `getting-started/index.md` and this repository's `README.md` |
| `AGENTS.md` | AGENT | Governs skill and product edits | Read automatically for product-repository work | Repository-root instruction path | Do not migrate; human contributor rules must be rewritten, not copied as agent policy | Yes | `development/index.md` and `contributing/index.md` (explanation only) |
| `CHANGELOG.md` | HUMAN | None | None | Explicit release-archive entry and asserted by tests | Copy or transform release history; product remains canonical | Yes | `reference/releases-and-versioning.md` |
| `CONTRIBUTING.md` | HUMAN | Mentions skill/eval authoring constraints | Defers to root `AGENTS.md` | Product contribution entry point; no runtime loader | Migrate and expand; later leave a short product pointer if desired | No | `contributing/index.md` |
| `LICENSE` | HUMAN | None | None | Explicit release-archive entry and legal distribution file | Copy for this repository under the same project policy | Yes | `LICENSE` |
| `NOTICE.md` | HUMAN | None | None | Explicit release-archive entry and product notice | Summarize or link; do not replace product notice | Yes | `security/third-party-and-notices.md` |
| `SECURITY.md` | HUMAN | None | None | GitHub security-policy convention; links to product security details | Expand human reporting and supported-version guidance | Yes | `security/reporting.md` |
| `THIRD-PARTY-NOTICES.md` | HUMAN | None | None | Explicit release-archive entry; integration attribution | Copy/rewrite for readers while product distribution notice stays canonical | Yes | `security/third-party-and-notices.md` |
| `.github/pull_request_template.md` | DUAL-USE | None | Contributor agents may encounter it during PR work | GitHub consumes this exact path | Do not migrate as documentation; explain contribution expectations separately | Yes | `contributing/pull-requests.md` (explanation only) |

## Existing product `docs/`

| Product source | Audience | Skill references | Agent references | Runtime/path sensitivity | Human migration or copy | Must remain | Proposed human destination |
|---|---|---|---|---|---|---|---|
| `docs/architecture.md` | HUMAN | None | None | Included because release packaging recursively includes `docs/`; linked from product README | Migrate and expand | No | `architecture/index.md` |
| `docs/configuration.md` | HUMAN | None | None | Release-packaged and linked from product README/JEV page | Migrate and expand against canonical schemas | No | `guides/configuration.md` |
| `docs/evaluation.md` | HUMAN | Mentioned by human skill-authoring guidance, not loaded by a skill | None | Release-packaged and linked from product README | Rewrite to separate product smoke checks from metrics-owned evaluation | No | `metrics/index.md` and `development/evaluation.md` |
| `docs/installation.md` | HUMAN | None | None | Release-packaged; linked from README and cited by durable audits | Split into task pages; keep commands verified | No | `getting-started/install.md`, `getting-started/update.md`, `getting-started/uninstall.md` |
| `docs/jev.md` | DUAL-USE | Linked by `jev-judgment/references/primitives.md` for examples and endpoint controls | A skill can follow the product-relative link | Product-relative path is an active runtime reference; also release-packaged | Write a separate human explanation; do not move until the product reference is made self-contained or redirected product-locally | Yes | `concepts/jev.md` |
| `docs/model-routing.md` | HUMAN | None | None | Release-packaged; configuration is advisory | Migrate and combine with the intelligence hierarchy | No | `concepts/model-routing.md` |
| `docs/project-integration.md` | HUMAN | None | None | Release-packaged; README links it and it points to product templates | Migrate and expand; canonical templates remain in product | No | `guides/project-integration.md` |
| `docs/release-process.md` | HUMAN | `release-verify` describes adjacent runtime behavior but does not load this file | None | Release-packaged and referenced in internal audit evidence | Migrate contributor process; link back to canonical workflow/config | No | `development/releases.md` |
| `docs/security.md` | HUMAN | Security skills express related rules but do not load it | None | Release-packaged; root security policy and audit evidence link it | Migrate and expand without copying sensitive artifacts | No | `security/index.md` |
| `docs/skill-authoring.md` | HUMAN | Describes all skills but is not a runtime skill reference | None | Release-packaged | Migrate as contributor guidance | No | `development/skill-authoring.md` |
| `docs/token-efficiency.md` | HUMAN | Related to skill design; no direct loader | None | Release-packaged | Migrate into concepts and evaluation methodology | No | `concepts/context-and-cost.md` |
| `docs/troubleshooting.md` | HUMAN | None | None | Release-packaged and linked from product README | Migrate and expand | No | `troubleshooting/index.md` |
| `docs/upstream-integrations.md` | HUMAN | Skills mention upstream tools but do not load this file | None | Release-packaged; linked from product README | Migrate as human integration policy | No | `architecture/upstream-integrations.md` |

## Installed instructions, runtime references, and skills

| Product source | Audience | Skill references | Agent references | Runtime/path sensitivity | Human migration or copy | Must remain | Proposed human destination |
|---|---|---|---|---|---|---|---|
| `global/AGENTS.md` | AGENT | Routes use of all toolkit skills and JEV fallback | Installed to the user's Codex `AGENTS.md`; explicitly loads the v2 baseline for ecosystem questions | Installer and tests require the exact product path | Explain behavior only | Yes | `concepts/index.md` and `reference/agents.md` |
| `plugins/codex-toolkit/references/v2-baseline.md` | AGENT | Ecosystem/roadmap reference for runtime work | Explicitly loaded by `global/AGENTS.md`; existence asserted by metadata tests | Plugin-relative reference and release payload | Summarize ownership and baseline for humans; never replace runtime file | Yes | `architecture/repository-boundaries.md` and `reference/releases-and-versioning.md` |
| `plugins/codex-toolkit/skills/address-pr-review/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Name, frontmatter, UI metadata, eval, installer, and validation must stay aligned | Document trigger and limits | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/agent-maintenance/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and limits | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/api-compatibility/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and limits | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/architecture-change/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and limits | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/benchmark/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and limits | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/dependency-change/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and limits | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/diagnostics/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and privacy limits | Yes | `reference/skills.md` and `security/artifacts.md` |
| `plugins/codex-toolkit/skills/docs-impact/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and cross-repository doc workflow | Yes | `reference/skills.md` and `contributing/documentation.md` |
| `plugins/codex-toolkit/skills/dotnet-format/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and limits | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/dotnet-verify/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and limits | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/finish-pr/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger, authorization, and non-merge behavior | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/issue-start/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and Git safety | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/jev-judgment/SKILL.md` | AGENT | Runtime skill; explicitly loads its two compact references | Installed/discovered through the plugin skill directory; implicit invocation disabled in UI metadata | Skill path and relative reference paths are runtime-critical | Write a human JEV explanation without copying this as prose documentation | Yes | `reference/skills.md` and `concepts/jev.md` |
| `plugins/codex-toolkit/skills/jev-judgment/references/primitives.md` | AGENT | Explicitly loaded by `jev-judgment` for request shape | Read lazily by the active agent; links product-relatively to `docs/jev.md` | Compact runtime reference; relative paths are critical | Explain separately; never move | Yes | `concepts/jev.md` |
| `plugins/codex-toolkit/skills/jev-judgment/references/thresholds.md` | AGENT | Explicitly loaded by `jev-judgment` for calibration | Read lazily by the active agent; points to product `config/jev.json` | Compact runtime reference; config relationship is critical | Explain and contextualize thresholds separately; never move | Yes | `concepts/jev.md` and `guides/configuration.md` |
| `plugins/codex-toolkit/skills/package-audit/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory; implicit invocation disabled in UI metadata | Same skill-directory contract | Document trigger and limits | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/performance-investigation/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and artifact handling | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/prepare-commit/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and Git safety | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/release-verify/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and incomplete-gate caveat | Yes | `reference/skills.md` and `development/releases.md` |
| `plugins/codex-toolkit/skills/repo-health/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract; reads product config | Document trigger and policy source | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/reproducible-build/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and cost | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/roadmap-next/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and deterministic ordering | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/sbom/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and output ownership | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/security-scan/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and source/privacy boundary | Yes | `reference/skills.md` and `security/index.md` |
| `plugins/codex-toolkit/skills/test-quality/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and on-demand costs | Yes | `reference/skills.md` |
| `plugins/codex-toolkit/skills/versioning/SKILL.md` | AGENT | Runtime skill definition (self) | Installed/discovered through the plugin skill directory | Same skill-directory contract | Document trigger and policy limits | Yes | `reference/skills.md` and `reference/releases-and-versioning.md` |

## Project templates

| Product source | Audience | Skill references | Agent references | Runtime/path sensitivity | Human migration or copy | Must remain | Proposed human destination |
|---|---|---|---|---|---|---|---|
| `templates/project/AGENTS.md` | AGENT | Routes project-local application of toolkit skills | Copied and completed as project-local agent instructions | Template path is declared in ecosystem config and release-packaged | Explain how to customize; do not make docs copy canonical | Yes | `guides/project-integration.md` |
| `templates/project/README.agent.md` | DUAL-USE | Describes skill/instruction integration | Read by adopters and potentially by agents in copied templates | Template bundle and release path | Rewrite as an integration guide | Yes | `guides/project-integration.md` |
| `templates/project/.github/pull_request_template.md` | DUAL-USE | None | Contributor agents may use it after template adoption | Copied to GitHub's path in target repositories | Explain fields; template remains canonical in product | Yes | `guides/project-integration.md` and `contributing/pull-requests.md` |

## Durable results and internal evidence

These records are deliberately not migration sources. They may contain revision-specific
evidence, operational details, or context that is unsuitable for public guidance. Later
human docs may restate verified, sanitized conclusions only.

| Product source | Audience | Skill references | Agent references | Runtime/path sensitivity | Human migration or copy | Must remain | Proposed human destination |
|---|---|---|---|---|---|---|---|
| `.agent-results/README.md` | INTERNAL-MACHINE | Diagnostics/performance skills may refer to selected results, not this prose directly | Generated by `results init`; normal discovery excludes the directory | Exact result-store path and generated content are tested | Do not migrate | Yes | None |
| `.agent-results/audits/20260921T195122Z-structural-completeness-2026-09-21.md` | INTERNAL-MACHINE | Evidence mentions several skills | Durable agent audit | Timestamped result-store path; excluded from normal discovery/releases | Do not copy raw audit; synthesize verified conclusions only | Yes | None |
| `.agent-results/audits/20260921T201733Z-codex-instructions-usage-cost.md` | INTERNAL-MACHINE | Audits all runtime skills and JEV references | Durable agent audit | Same result-store constraints | Do not copy raw audit; use sanitized conclusions in concepts/metrics if still valid | Yes | None |
| `.agent-results/audits/20260921T202752Z-skills-agents-token-efficiency-2026-09-21.md` | INTERNAL-MACHINE | Audits skills and agents | Durable agent audit | Same result-store constraints | Do not copy raw audit | Yes | None |
| `.agent-results/handoffs/20260921T192544Z-phase-1-results-infrastructure.md` | INTERNAL-MACHINE | None | Cross-chat agent handoff | Same result-store constraints | Do not migrate | Yes | None |
| `.agent-results/handoffs/20260921T194238Z-phase-2-credential-boundary.md` | INTERNAL-MACHINE | JEV-related context | Cross-chat agent handoff | Same result-store constraints | Do not migrate; restate only verified public security behavior | Yes | None |
| `.agent-results/handoffs/20260921T202752Z-skills-agents-token-efficiency-2026-09-21.md` | INTERNAL-MACHINE | Skill-efficiency context | Cross-chat agent handoff | Same result-store constraints | Do not migrate | Yes | None |
| `.agent-results/reports/20260921T203821Z-end-to-end-dogfood.md` | INTERNAL-MACHINE | Product workflow evidence | Durable agent report | Same result-store constraints | Do not migrate raw results | Yes | None |
| `.agent-results/reports/20260921T205325Z-jev-integration-validation.md` | INTERNAL-MACHINE | JEV integration evidence | Durable agent report | Same result-store constraints; live/private handling concerns | Do not migrate raw results; use only sanitized, reproducible claims | Yes | None |
| `.agent-results/reviews/20260921-final-adversarial-release-readiness.md` | INTERNAL-MACHINE | Findings cite runtime skills and docs | Durable agent review | Same result-store constraints | Do not migrate raw review | Yes | None |

## Test fixtures

| Product source | Audience | Skill references | Agent references | Runtime/path sensitivity | Human migration or copy | Must remain | Proposed human destination |
|---|---|---|---|---|---|---|---|
| `tests/fixtures/binlogs/README.md` | INTERNAL-MACHINE | Diagnostics guidance is adjacent but does not load it | Test/developer-only fixture guidance | Fixture-relative path; tests and contributor setup own it | Do not migrate; explain safe artifact handling separately if useful | Yes | `security/artifacts.md` (new explanation only) |
| `tests/fixtures/git/README.md` | INTERNAL-MACHINE | Git workflow skills are adjacent but do not load it | Test/developer-only fixture guidance | Fixture-relative path | Do not migrate | Yes | None |
| `tests/fixtures/msbuild/build-failure.txt` | INTERNAL-MACHINE | None | Parsed as test input | Exact fixture path/content may be used by tests | Do not migrate | Yes | None |
| `tests/fixtures/msbuild/build-success.txt` | INTERNAL-MACHINE | None | Parsed as test input | Exact fixture path/content may be used by tests | Do not migrate | Yes | None |

## Migration order and guards

1. Build the human pages from the destinations above by rewriting for tasks and readers.
2. Keep product runtime references, skills, instructions, templates, fixtures, and legal
   distribution files in place.
3. Before removing any `Must remain: No` source, search product code, tests, workflows,
   release packaging, Markdown links, skills, and agents again at the then-current revision.
4. Update product-local links and release behavior in a product-owned phase. This docs
   repository must never become a runtime dependency.
5. Validate that JEV's skill-loaded compact references still resolve locally in the
   product repository and that uncertainty continues to route to Codex.

## Baseline import status

The human rewrite was completed against product commit `a7e2515` on `develop/v2.0.0`.
The pages under `getting-started/`, `guides/`, `concepts/`, `architecture/`, `reference/`,
`security/`, `metrics/`, `troubleshooting/`, `development/`, `contributing/`, and
`examples/` now cover the destinations above. Closely related proposed destinations were
combined where one task-oriented page is clearer; for example repository boundaries are
part of `architecture/index.md`, artifact privacy is part of `security/index.md`, and
pull-request expectations are part of `contributing/index.md`.

No runtime file was moved, deleted, or redirected. In particular, the JEV skill and its
compact references remain product-local. Older source prose that described three agents
or 25 skills was not carried forward: the verified baseline contains one native reviewer
agent and 24 skill directories. Release status is linked to the product repository rather
than inferred from roadmap branch names.
