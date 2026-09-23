# JEV and bounded judgment

JEV is an optional semantic classification layer backed by TypeSafe's API. It is useful
when deterministic filtering has already narrowed a set but reading every candidate with
a general model would be wasteful. It is not an authorization system, architecture
decision-maker, secret scanner, or substitute for Codex.

AgentTool supports Noul probability, Choice, ordered Score, and candidate screening.
Responses are checked for expected types, ranges, and distributions before they can be
used. The default policy maps Noul values at or above `0.70` to `INCLUDE`, values at or
below `0.10` to `EXCLUDE`, and the middle to `REVIEW`. Choice and Score need at least
`0.80` confidence. These values come from `config/jev.json` and need task-specific
calibration.

## Safe request flow

Prepare a small, sanitized input:

```json
{"state":"README describes build setup","instructions":"Is this relevant to build documentation?"}
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

`--safe-input` records caller review; it is not automated data-loss prevention. Never
send credentials, `.env` content, whole private repositories, or unnecessary excerpts.
Screen candidates must have unique non-empty IDs and text, and should be narrowed before
submission.

## Failure, modes, and cache

`auto` and `off` preserve normal Codex fallback. Missing credentials, malformed answers,
service failure, and uncertain judgments become `REVIEW`; `required` mode additionally
uses exit code 3 for service failure. Requests are not automatically retried.

The best-effort cache hashes the canonical request and endpoint and stores responses,
not requests or keys. Its default lifetime is 24 hours; set `cacheHours` to `0` to
disable it or run `jev cache-clear`. Responses can still be sensitive. Model aliases may
change, so pin a provider model when repeatability matters.

The runtime's compact JEV references remain in the
[`jev-judgment` skill](https://github.com/simplexidev/codex-toolkit/tree/develop/v2.0.0/plugins/codex-toolkit/skills/jev-judgment);
this page is an independent human explanation.
