# Context and token efficiency

The toolkit optimizes the amount of information made visible to a model while preserving
the evidence needed for a correct result. The target is not the smallest transcript at any
cost. A short run that misses a defect, skips a safety invariant, or validates the wrong
project is worse than a longer correct run.

## Load progressively

There are several distinct context surfaces:

- **Always visible:** brief plugin discovery metadata and applicable instructions.
- **Activation visible:** the selected skill's complete workflow.
- **Lazy:** compact references loaded only for a branch of that workflow.
- **Local evidence:** logs, SARIF, test results, and reports kept on disk and summarized.
- **Isolated agent context:** task-specific evidence delegated to a justified native agent.

A capability can therefore be broad without every capability's instructions being loaded
into every task. Short routing descriptions decide whether to activate a skill; they are
not compressed substitutes for its safety rules.

## Narrow before reasoning

An efficient workflow usually does the following:

1. Search filenames and symbols before opening files.
2. Ask AgentTool for exact changed paths, ownership, project graphs, or bounded artifact
   summaries.
3. Select affected builds and tests instead of defaulting to the entire repository.
4. Keep large raw artifacts local and open only the evidence relevant to the failure.
5. Use JEV only on a small residual classification that passed local policy checks.
6. Use GPT reasoning for interpretation, generation, and genuinely hard uncertainty.
7. Delegate only when an independent context has a measured quality or isolation benefit.

This ordering avoids spending model context to rediscover facts a deterministic parser can
provide. It also avoids treating semantic confidence as an exact repository fact.

## Static cost versus run cost

Static cost estimates the content that could be exposed: routing metadata, skill files,
lazy references, and agent instructions. Run cost observes a particular execution:
provider tokens when available, turns, tool calls, files or context, elapsed time, build
and test breadth, and subagent usage. A low static maximum does not guarantee a cheap run,
and a high maximum is not paid when its lazy references never load.

The metrics analyzer reports exact UTF-8 byte and character counts but estimates tokens as
`ceil(UTF-8 bytes / 4)` when no provider tokenizer is available. Those token values must
remain labeled `estimated`, not presented as billing measurements.

## Quality before efficiency

Compare cost only after checking completion, deterministic and safety assertions, semantic
quality, correct skill activation and delegation, tool use, nested-delegation limits, and
context isolation. The evaluation record keeps these as explicit quality fields and a
final gate. Regression history separately labels quality, tokens, tools, files/context,
validation breadth, routing, delegation, JEV, capability coverage, noise, and insufficient
samples.

Efficiency is evidence for choosing between quality-compatible approaches. It is not an
excuse to skip required validation, discard uncertain candidates, or replace an exact
check with a cheaper guess. See the [evaluation methodology](../metrics/methodology.md).
