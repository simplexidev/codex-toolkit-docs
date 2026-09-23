# Security, credentials, and privacy

The toolkit is designed to reduce accidental mutation and data exposure, not to defend
against a malicious process running as the same user. Keep the checkout, target
repositories, and user profile trusted.

## Execution and Git boundaries

AgentTool launches child processes with argument arrays rather than a shell and enforces
timeouts. Branch creation requires a clean, attached repository with no in-progress Git
operation and an appropriate open issue. PR preparation never commits, pushes, publishes,
or merges. GitHub commands use the user's existing `gh` authentication.

MSBuild and build commands may execute project or imported logic. Run them only for
trusted repositories. Optional tools and upstream integrations are not installed
automatically.

## Installation boundary

The installer records exact links and removes only matching, owned entries. It refuses
symlinked state and destination parents to reduce redirected writes. Replacements and
unrelated files are preserved. A same-user filesystem race remains outside this model.

## The JEV credential

`TYPESAFE_API_KEY` is the only application-level secret input. AgentTool accepts it only
from its own environment, removes it from every child-process environment, and does not
accept it in arguments, configuration, request JSON, logs, cache entries, or structured
output. Only the JEV HTTP path can apply it as bearer authentication, and redirects are
disabled.

Inject the key only into the specific AgentTool process or a narrowly scoped terminal
session. Secret storage and injection are outside the toolkit. Do not put it in a
repository, `.env`, JSON, shell profile, `environment.d`, desktop-wide environment, or
the input payload. `doctor` reports only whether JEV credentials are available.

Normal tests and CI are keyless and use fake HTTP responses. Any live GitHub check should
use the dedicated protected `jev-integration` environment, trusted manual or low-frequency
scheduled triggers, and no fork pull-request exposure.

## Artifacts and privacy

Full logs, traces, dumps, binlogs, SARIF, and JEV responses can contain private source,
paths, tokens, or user data even when terminal summaries are redacted. `.agent-tool/` and
generated `.agent-results/` content should stay ignored and local. Review and sanitize
before sharing; do not publish raw prompts, responses, transcripts, or private source.

JEV's heuristic secret detection is defense in depth, not a DLP system. Send the minimum
reviewed excerpt and route uncertainty back to Codex. See [JEV](../concepts/jev.md).

## Report a vulnerability

Do not open a public issue containing credentials, private source, dumps, or exploit
details. Use the product repository's private vulnerability reporting feature when
available; otherwise ask maintainers for a private channel before disclosing details.
The canonical supported-version policy is the product's
[`SECURITY.md`](https://github.com/simplexidev/codex-toolkit/blob/develop/v2.0.0/SECURITY.md).
