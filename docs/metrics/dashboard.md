# Interpreting the metrics dashboard

Open the dashboard at <https://simplexidev.github.io/sdeveng-metrics-dashboard/> once the
repository split is complete; during migration it remains at
<https://simplexidev.github.io/codex-toolkit-metrics/>. It is a view
of manifest-approved public aggregates, not a live telemetry console and not an input to
the toolkit runtime.

## Current v2 status

The current v2 public dashboard contains reviewed static-cost, baseline, and agent-capability
aggregates. It does **not** publish a v2 release-acceptance result. The earlier acceptance
snapshot was withdrawn after final review because its evaluation matrix, capability mapping,
and evidence coverage were not sufficient for a release decision. Do not use the dashboard to
claim that v2 is release-ready, that the custom reviewer was exercised in delegation, or that
JEV produced a measured context benefit. The metrics repository's
[`v2 acceptance status`](https://github.com/simplexidev/codex-toolkit-metrics/blob/v2.0.0/reports/v2-acceptance.md)
records the withheld decision and the conditions for a future acceptance publication.

## Read a result in this order

1. Confirm the subject repository and revision, generation time, scenario count, and
   provenance approval.
2. Identify the exact arms. `UPSTREAM` means the plan's pinned overlay; `OPTIMIZED` means
   the named toolkit/candidate configuration; agent arms have a separate customization
   dimension.
3. Check completion, assertions, semantic quality, safety, routing, delegation, and context
   isolation before cost.
4. Check repetitions, source-run count, compatibility, and any insufficient-sample label.
5. Read each metric's unit, direction, evidence kind, and method.
6. Only then compare tokens, tools, elapsed time, context, validation breadth, or static
   cost.

“Higher is better” and “lower is better” describe a metric's local direction, not the whole
system. Fewer tool calls may be good after equivalent quality; they may also reveal that an
arm skipped validation. More delegation may show correct isolation or unnecessary fan-out.

## Static-cost panels

Static reports distinguish the always-visible routing surface, activation-visible skill
content, lazy references, maximum possible load, trigger overlap, and agent configuration
and instructions. Exact byte/character inventory is measured. Token values are estimates
using the disclosed bytes/4 approximation. Maximum possible load is not the context paid
by every request.

Routing overlap is a structural signal, not a routing-accuracy result. Use execution
scenarios to assess false and missed activation/delegation. Ambiguous cases may be observed
without being scored.

## Baseline and agent panels

The pre-optimization baseline preserves evidence from before later changes. It is a
comparison anchor, not a promise that its arm is currently recommended. One repetition per
arm provides broad coverage but little statistical power; interpret small differences
cautiously.

Agent-capability panels compare built-in/generic, current, historical, and candidate
behavior only for the cited scenarios. A `keep`, `retire`, `replace`, or
`insufficient-evidence` disposition is a reviewed conclusion over those records. Candidate
instructions live in the evaluator until a separate product change adopts them.

## Metric labels

- `measured` is directly observed by the named method.
- `derived` is calculated from validated inputs.
- `estimated` is an approximation whose method matters.
- `unavailable` is represented in detailed evaluation records as null and must not be read
  as zero; public dashboard aggregates omit unavailable numeric values.

Synthetic approval means the artifact demonstrates the measurement and publication path
with synthetic inputs. Reviewed approval means a human approved the sanitized aggregate;
it does not turn a small or narrow sample into a universal benchmark.

The production dashboard excludes synthetic demonstration fixtures. A displayed reviewed
aggregate still has the scope, source revision, and approval shown with it; only artifacts
in a compatible series should be interpreted as a trend.

## Limitations and non-claims

The dashboard does not claim:

- that performance transfers to private repositories, other languages, prompts, models,
  Codex CLI versions, or toolchains;
- that an estimated token count equals provider billing or tokenizer output;
- that elapsed time is stable across machines, network conditions, caches, or service load;
- that a semantic judge is ground truth or free of position/model bias;
- that a passing aggregate proves security, privacy, correctness, or complete capability
  coverage;
- that upstream HEAD, every upstream plugin, or every custom-agent candidate was tested;
- that correlation between a toolkit feature and an outcome establishes causation outside
  the controlled arms;
- that sanitized public data is sufficient to reproduce private raw model responses.

Use the dashboard to locate evidence and trends. Use the versioned plan, schema, public
artifact, provenance, and methodology to decide how strong a conclusion that evidence can
support.
