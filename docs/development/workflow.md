# Five-repository development workflow

SimplexiDev Engineering Toolkit development uses five sibling repositories. Keep them beside one another
so product, documentation, and evaluation work can be inspected together without making
any repository a runtime dependency of another:

```text
workspace/
├── sdeveng/                  # product runtime
├── sdeveng-docs/              # this human documentation site
├── sdeveng-metrics-tooling/   # evaluator, schemas, and measurement code
├── sdeveng-metrics-data/      # reviewed sanitized aggregates
└── sdeveng-metrics-dashboard/ # static dashboard and Pages workflow
```

Local runner and prompt state may live in `.agent-results/prompts/` next to those
repositories. It is local state: do not commit, move, delete, or publish it.

## Pick the owning repository

`sdeveng` owns one unified Codex plugin, one project template, `AgentTool`, runtime
skills, compact agent-consumed references, native/custom agent metadata and evidence,
JEV integration, installers, tests, and releases. Runtime references stay there even when
they are Markdown. Before moving any product document, search its consumers; a skill or
agent-loaded reference must remain product-local.

`sdeveng-docs` owns explanations for people: installation, configuration, examples,
architecture, security, contributor guidance, and metrics methodology. It is never a
runtime input. Explain runtime material here in human terms rather than copying a compact
skill reference or `AGENTS.md`.

`sdeveng-metrics-tooling` owns evaluator code, scenarios, schemas, and statistics.
`sdeveng-metrics-data` owns reviewed sanitized aggregates, while
`sdeveng-metrics-dashboard` owns static presentation and publishes
<https://simplexidev.github.io/sdeveng-metrics-dashboard/>. The repositories cooperate
through versioned files and explicit checkout paths; none is a plugin or product runtime
dependency.

## Start and finish a change

Read the `AGENTS.md` in the repository you will modify. Those files are instructions for
coding agents and repository automation; this site is the human explanation. Do not copy
an entire `AGENTS.md` into these pages. Inspect status and remotes before changing files
and preserve unrelated work.

After each repository has its initial commit, use its designated integration base:

1. Fetch and prune, then start clean from the current base. Product v3 work targets
   `develop/v3.0.0`; docs and metrics work also target their corresponding
   `develop/v3.0.0` integration line.
2. Create one fresh branch named `roadmap/<phase-slug>` for one focused phase.
3. Make changes only in the repository that owns the phase. Sibling repositories may be
   read for verification.
4. Run the relevant checks, inspect rendered documentation when applicable, and commit.
5. Push the branch and create or update one pull request to the designated base. Describe
   scope, validation, security/privacy impact, and any intentionally deferred gate.
6. Wait for required checks and required approval. Merge if policy and permissions allow,
   synchronize the base, then delete the merged local branch and, when allowed, its remote
   branch.

If approval is required, keep the existing pull request and resume it after approval;
never open duplicate branches or PRs. A first, truly empty docs or metrics repository may
receive its bootstrap default-branch commit directly. Do not force-push, rewrite tags, or
leave a merge, rebase, cherry-pick, or revert unfinished.

## Build, test, format, and validate

Run commands from the checkout they name. These are the normal keyless gates, not a claim
that every optional release or live integration check has run.

For the product (requires .NET 10):

```console
dotnet test tests/SdevEng.Tests/SdevEng.Tests.csproj
dotnet tools/AgentTool.cs validate
dotnet tools/AgentTool.cs eval
dotnet format tests/SdevEng.Tests/SdevEng.Tests.csproj --no-restore --verify-no-changes
git diff --check
```

`AgentTool` is the product's single .NET utility. Prefer extending it with small,
structured, composable commands over adding helper scripts or asking a model to infer
facts that tooling can compute. Add focused unit tests for changed behavior; keep command
schemas, configuration, manifests, installer/update/uninstall behavior, and human docs
synchronized. Installer tests must use temporary homes, never a real Codex profile.

For metrics (using the SDK selected by `global.json`):

```console
dotnet restore SdevEng.Metrics.slnx
dotnet test SdevEng.Metrics.slnx
dotnet run --project src/SdevEng.Metrics -- validate-evaluation tests/SdevEng.Metrics.Tests/Fixtures/evaluation-valid-v1.json
dotnet run --project sdeveng-metrics-tooling/src/SdevEng.Metrics -- validate-public sdeveng-metrics-data/public/example-summary.json
dotnet run --project sdeveng-metrics-tooling/src/SdevEng.Metrics -- dashboard-check sdeveng-metrics-dashboard
dotnet run --project sdeveng-metrics-tooling/src/SdevEng.Metrics -- publish-pages sdeveng-metrics-dashboard sdeveng-metrics-data/public _site
dotnet format SdevEng.Metrics.slnx --no-restore --verify-no-changes
```

For this documentation repository, verify links and Markdown formatting, review the
rendered pages, and verify behavioral claims against product code, schemas, tests, or a
selected release. Update `docs/migration-manifest.md` if a source's audience, ownership,
or consumers change.

## Design for narrow, efficient use

Use this order of decision-making:

1. **Deterministic AgentTool or structured tooling** for exact facts, parsing, validation,
   affected-path selection, and repeatable execution.
2. **JEV** for a bounded semantic choice with a tiny reviewed payload, thresholds, call
   limits, and a safe `REVIEW` outcome.
3. **Codex reasoning or generation** for work that needs broader synthesis.
4. **A stronger reasoning model** only when the evidence shows it is justified.

Do not use JEV for authorization, exact facts, or as an always-on substitute for
deterministic checks. A skill is appropriate for a recurring workflow with a precise
trigger; keep its instructions short, route with tiny metadata, and load detailed
references lazily. A custom agent needs evidence that a narrowly scoped role improves the
outcome; use few such agents, bounded delegation, isolated context, and measured routing
cases. Broad capability coverage is not a reason to load broad context.

Every new or changed skill needs a realistic positive scenario, a negative trigger, and
a safety invariant in product `evals/`. Offline `AgentTool eval` checks scenario integrity;
it is not proof of quality. Meaningful changes also need measurements that compare
correctness before cost: tokens, turns, tool calls, elapsed time, files/context read,
routing, delegation, and unnecessary broad operations. Evaluators and judges are
OpenAI/GPT only—do not add Claude execution or judging. See [skill authoring](skill-authoring.md)
and [metrics and evaluation](../metrics/index.md).

## Provenance, releases, and publication

Use .NET/BCL facilities unless a dependency has a documented correctness or
interoperability reason. Follow upstream .NET provenance and license obligations: retain
required notices, record source/version/license information, do not vendor upstream
content casually, and review the actual package or version before redistribution. The
product's [third-party notices](../security/third-party-and-notices.md) are the human
starting point, not a substitute for that review.

For a product release, synchronize the semantic version in `config/toolkit.json` and
plugin manifests, run the full required gate, review schemas, notices, changelog, and
package contents, and create/push `vMAJOR.MINOR.PATCH` only with explicit authorization.
The release workflow creates a draft source release and SHA-256 checksum for review. Do
not package tests, caches, local prompt state, private metrics, or result stores. See
[release process](releases.md) and [releases and versioning](../reference/releases-and-versioning.md).

Metrics publication is more restrictive: normal CI is synthetic or mocked and keyless;
raw runs, prompts, responses, transcripts, private source, and logs stay ignored locally
or in short-lived CI artifacts. Commit and publish only reviewed, schema-valid sanitized
aggregates allowed by the metrics publication manifest. Check dashboard output before it
is deployed and keep its paths compatible with the project Pages base.

## Secrets and security reports

Never commit or paste secrets, raw private source, prompts, responses, local absolute
paths, or unsanitized logs into a PR, release, documentation, public data, or dashboard.
`TYPESAFE_API_KEY` must be read only at the JEV authorization boundary: never persist,
print, serialize, echo, or pass it to unrelated subprocesses. Normal JEV tests and CI
use fake HTTP and no key; a deliberately scoped live check is the exception.

Report a security issue through the product repository's
[private vulnerability reporting channel](https://github.com/simplexidev/sdeveng/security/advisories/new)
and include only a minimal sanitized reproduction. If that channel is unavailable, ask a
maintainer for a private channel. Do not disclose an unpatched vulnerability in a public
issue or evaluation artifact.
