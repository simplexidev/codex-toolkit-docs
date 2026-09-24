# Runtime data flows

This page identifies what crosses each runtime boundary. It is descriptive, not an API
contract; the installed product's schemas and command help remain canonical.

## Discovery and routing

Codex begins with its normal instruction discovery. The toolkit's installed global policy
and an adopting repository's project instructions provide broad constraints. Plugin
metadata exposes short skill names and descriptions for routing. A selected skill then
loads its complete `SKILL.md`; supporting references are opened only when that workflow
requires them.

The plugin is not a daemon and does not receive every prompt. Skills are guidance in the
active Codex context. AgentTool is invoked as a child command for structured work, and a
native agent is a separate Codex context selected by the root agent when its narrow role is
justified.

## Exact local work

For repository, Git, GitHub, .NET, artifact, lifecycle, and result-store commands, the flow
is:

```text
bounded CLI arguments
  -> validate root, configuration, and command preconditions
  -> inspect files or launch an argument-array child process
  -> parse and normalize output
  -> return bounded text or structured JSON
  -> store oversized evidence under ignored local artifact paths
```

Child processes are launched without a shell, with redirected output and timeouts. This
reduces quoting and accidental-expansion risk; it does not make an untrusted build safe.
MSBuild targets, test adapters, repository hooks, and tools can execute project-controlled
code. Full evidence stays local while the model receives a compact summary and an explicit
path when deeper inspection is needed.

Mutation is command-specific. Inspection and planning commands do not silently graduate
to write, publish, or merge operations. For example, PR preparation is distinct from
committing, pushing, publishing, or merging.

## JEV judgment

JEV follows a different, explicitly external flow:

```text
local deterministic narrowing
  -> capability, purpose, size, count, and sensitivity checks
  -> dry-run renders the provider payload without sending it
  -> caller reviews the minimized payload and supplies --safe-input
  -> AgentTool reads TYPESAFE_API_KEY at the HTTP authorization boundary
  -> one bounded HTTPS request, with redirects disabled
  -> response type/range/confidence validation
  -> INCLUDE / EXCLUDE / REVIEW, with uncertainty returning to Codex
```

Routing fields such as capability and purpose enforce local policy and are not provider
prompt content. The response cache is keyed by a hash of the canonical request and
endpoint; it stores a reduced response, not the request or credential. Cache contents may
still reveal a sensitive classification and remain local.

See [JEV and bounded judgment](../concepts/jev.md) and the
[credential and subprocess boundary](../security/jev-credentials-and-subprocesses.md).

## Native-agent delegation

A native agent receives only the task and evidence needed for its role. The current
reviewer is read-only and intended for an explicitly requested review or a substantial,
high-risk completed diff. It reports findings to the root agent and cannot edit, merge, or
delegate again. This isolation can improve independent review, but it also costs another
context and is therefore measured rather than assumed to be beneficial.

Candidate and retired agent instructions may appear in the metrics repository as
evaluation overlays. They are not installed product agents. A dashboard comparison is
evidence about a bounded scenario set, not an instruction to install every candidate.

## Installation and update

AgentTool calculates desired links from a selected toolkit checkout to the user's Codex
locations, validates parents and link safety, and records owned entries in an installation
manifest. Update reconciles those owned entries. Uninstall removes only entries that still
match the recorded ownership; user replacements and unrelated files survive.

Marketplace registration is a parallel discovery route for the plugin only. It does not
complete the global-instruction or native-agent installation flow.

## Metrics flow is offline from the product

The metrics runner creates isolated fixture copies, overlays the arm's selected skills or
agent configuration, runs the OpenAI-backed Codex CLI, applies deterministic assertions,
and invokes bounded judging only when configured. Raw events and responses go to ignored
private storage. A separate aggregation and publication path emits reviewed, schema-valid,
sanitized data for the dashboard.

No dashboard request, evaluation plan, or metrics history participates in an ordinary
toolkit task. This one-way relationship prevents documentation or public metrics from
becoming runtime control inputs.
