# JEV credentials and subprocesses

`TYPESAFE_API_KEY` has one intended destination: the `Authorization: Bearer` header on an
approved AgentTool JEV request. It must not become general process configuration.

## Safe injection

Prefer a secret manager or a one-command environment assignment so only the AgentTool
process receives the key. The exact injection mechanism depends on the operating system
and secret store. Do not paste a real value into issue text, shell history, documentation,
screenshots, or diagnostic output.

The key must not be placed in:

- command-line arguments or JEV input JSON;
- toolkit configuration, `.env` files, shell profiles, or repositories;
- Codex prompts, skill or agent instructions, logs, caches, or result records;
- a desktop-wide or service-wide environment shared with unrelated processes.

`doctor` reports only configured versus unavailable. It does not print or validate the
secret by making a billable call.

## AgentTool boundary

AgentTool reads the environment variable at the JEV HTTP authorization boundary. Redirects
are disabled so the bearer header is not followed to another origin. The caller must first
pass capability and purpose policy, deterministic narrowing, size/count checks, heuristic
sensitivity checks, and explicit `--safe-input` acknowledgement.

When AgentTool launches Git, `gh`, `dotnet`, or another child, it builds an argument array
without a shell and removes `TYPESAFE_API_KEY` from the inherited environment. It also
refuses a child argument containing the current key. This protects the normal subprocess
path; it does not stop another process running as the same user from inspecting the parent
environment or memory.

Do not deliberately forward the key through another variable, file, standard input, or
wrapper. That bypasses the designed boundary and may put the value in process listings,
logs, crash dumps, or build artifacts.

## Requests, responses, and cache

`--dry-run` constructs the outbound semantic payload without transmitting it. Review that
payload, minimize it, then make the live call with `--safe-input`. Local routing fields are
used for policy enforcement and are not semantic prompt content sent to the provider.

The cache key is a SHA-256 hash over the canonical request and endpoint. A cache entry
contains a reduced provider answer, not the request or key. It can still disclose the
classification, confidence, selected choice, or score and therefore belongs in ignored
local storage. Disable caching for sensitive work or clear it after the task when policy
requires.

## Failure behavior

Missing credentials, policy refusal, timeout, HTTP failure, malformed data, invalid ranges,
or insufficient confidence must not create a guessed positive or negative decision. In
normal `auto` or `off` operation the result routes to `REVIEW` and Codex. In `required`
mode a service failure also returns the documented non-success exit code. Requests are not
automatically retried, limiting surprise cost and duplicate disclosure.

Normal tests and CI use mocked HTTP responses and no key. Live checks require an explicit,
protected context and must never run for untrusted fork pull requests.
