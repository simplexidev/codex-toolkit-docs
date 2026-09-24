# JEV and bounded judgment

JEV is an optional semantic classification layer backed by TypeSafe's API. It is useful
when deterministic filtering has already narrowed a set but reading every candidate with
a general model would be wasteful. It is not an authorization system, architecture
decision-maker, secret scanner, or substitute for Codex.

## Position in the hierarchy

Use deterministic tooling for facts and rules. Use JEV for a bounded meaning question
whose allowed outcomes and fallback are known in advance. Use Codex/GPT for synthesis,
implementation, root-cause reasoning, and every unresolved JEV result. This separation
keeps a probabilistic answer from silently acquiring authority it does not have.

AgentTool supports Noul probability, Choice, ordered Score, and candidate screening.
Responses are checked for expected types, ranges, and distributions before they can be
used. The default policy maps Noul values at or above `0.70` to `INCLUDE`, values at or
below `0.10` to `EXCLUDE`, and the middle to `REVIEW`. Choice and Score need at least
`0.80` confidence. These values come from `config/jev.json` and need task-specific
calibration.

`noul` returns a probability and routes it to `INCLUDE`, `EXCLUDE`, or `REVIEW`.
`choice` selects among a named criteria object, and `score` selects an ordered criteria
array; both require at least two choices and sufficient confidence. `screen` applies the
same bounded policy to a pre-narrowed list of uniquely identified candidates. The local
input must declare a configured `capability`, an allowed `purpose`, and
`deterministicNarrowed: true`; those routing fields are not transmitted to the provider.

Each capability starts with an expected-call budget of zero, with a hard maximum when it
is permitted. The current permitted families are relevance, PR/SARIF triage, bounded
failure or upstream classification, and one ambiguous routing tie-break. Exact repository
facts and commands, authorization or security disposition, code generation, architecture,
and open-ended debugging are disallowed. A service response cannot override those bounds.

`expectedCalls: 0` means ordinary execution should succeed without a provider call; it is
not the same as a ban. The capability's `maxCalls`, input bytes, candidate count, privacy
label, purposes, minimum confidence, and deterministic-first requirement form the hard
local envelope. Configuration values are policy inputs, not evidence that a particular
task is safe to send.

## Safe request flow

Prepare a small, sanitized input:

```json
{"capability":"relevance","purpose":"docs-impact","deterministicNarrowed":true,"state":"README describes build setup","instructions":"Is this relevant to build documentation?"}
```

Inspect the request without transmitting it:

```console
dotnet tools/AgentTool.cs jev noul --input safe.json --dry-run
```

Only after reviewing that exact payload and injecting the credential through your chosen
narrow process boundary, make the live request:

```console
dotnet tools/AgentTool.cs jev noul --input safe.json --safe-input
```

`--safe-input` records caller review; it is not automated data-loss prevention. The
heuristic detector can refuse obvious secret-like material but cannot understand every
credential or privacy obligation. Never send credentials, `.env` content, whole private
repositories, raw logs, or unnecessary excerpts. Screen candidates must have unique
non-empty IDs and text and must be narrowed before submission.

The API credential is read from `TYPESAFE_API_KEY` only when AgentTool constructs the
authorized HTTP request. It is not accepted in CLI arguments, input JSON, or config, and
AgentTool removes it from every child-process environment. See the full
[credential boundary](../security/jev-credentials-and-subprocesses.md).

## Failure, modes, and cache

`auto` and `off` preserve normal Codex fallback. Missing credentials, malformed answers,
service failure, policy refusal, and uncertain judgments become `REVIEW`; `required` mode
additionally uses exit code 3 for service failure. Requests are not automatically retried.

The best-effort cache hashes the canonical request and endpoint and stores responses,
not requests or keys. Its default lifetime is 24 hours; set `cacheHours` to `0` to
disable it or run `jev cache-clear`. Responses can still be sensitive. Model aliases may
change, so pin a provider model when repeatability matters.

The cache changes latency and remote-call counts, so evaluation must record cache behavior
and compatibility rather than comparing a cached arm with an uncached arm as though they
were equivalent.

## Calibration and evaluation

Runtime thresholds are heuristics that need task-specific calibration. In the metrics
evaluator, deterministic assertions run first. A configured JEV rubric can resolve a
semantic case only when it returns an accepted, sufficiently confident score. Unavailable,
invalid, or low-confidence results escalate to the configured OpenAI GPT judge. Evaluation
records count JEV remote calls separately from GPT judge tokens, so a hybrid path is not
misreported as free.

Live paired calibration is explicit, private, and bounded to at most 50 labeled examples.
A confidence recommendation requires at least three observed examples at 90% expected-
outcome accuracy. This is a starting constraint, not proof of general validity; a new
purpose, model, threshold, or input distribution may require new calibration.

The runtime's compact JEV references remain in the
[`jev-judgment` skill](https://github.com/simplexidev/codex-toolkit/tree/develop/v2.0.0/plugins/codex-toolkit/skills/jev-judgment);
this page is an independent human explanation.
