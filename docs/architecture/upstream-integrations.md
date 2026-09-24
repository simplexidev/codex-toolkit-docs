# Upstream integrations

The toolkit references official .NET skills and optional diagnostic, compatibility,
security, and release tools through product manifests. Those entries express integration
policy; they are not vendored code, automatic installers, exhaustive version pins, or
verified setup recipes.

## Derivation and provenance

The canonical
[`upstream/dotnet-skills.json`](https://github.com/simplexidev/codex-toolkit/blob/develop/v2.0.0/upstream/dotnet-skills.json)
records the inspected `dotnet/skills` repository, branch, commit, inspection date, license,
inventory summary, and per-capability decisions. A decision can keep an upstream skill as
an independently installed reference, use deterministic toolkit functionality for exact
parts, retain GPT expertise for interpretation, or decline installation. The manifest also
records trigger, context-loading, tool/MCP, and rationale fields so a similar name is not
mistaken for copied implementation.

Toolkit skills may be derived from the problem decomposition learned during upstream
review, but upstream source is not vendored or silently rewritten into the unified plugin.
The product records the source revision and license for auditability. Users should still
verify the selected upstream revision and its current notices before installing or
redistributing it.

`upstream/versions.json` tracks repositories at a higher level; a `null` revision means an
unpinned reference whose current HEAD is reported for maintainer review, not a reproducible
dependency. `upstream/tools.json` is informational policy for optional tools, not a package
lock. A license label there is not a substitute for checking the exact package version.

## Context and installation policy

Upstream plugins remain separately installable. They are never bundled as additional
Codex Toolkit plugins, and the toolkit does not install an entire upstream marketplace.
Use compact decision metadata for routing, then load or install one upstream capability
only for an explicit task that benefits from it. This preserves the one-plugin architecture
and prevents broad capability coverage from imposing broad context cost.

`upstream status` reads the recorded policy. `upstream update --dry-run` can report what
would be checked without network access; a real update query uses GitHub CLI and writes a
review artifact under ignored `.agent-tool/`. Drift is reported for human review and is
never automatically merged.

Install third-party skills or tools separately from their current official instructions.
Check the selected version's license and notices before redistribution. The product's
[`upstream/`](https://github.com/simplexidev/codex-toolkit/tree/develop/v2.0.0/upstream)
directory is the canonical recorded policy.

An upstream comparison in metrics means the pinned overlay named by that evaluation plan.
It does not claim that every upstream skill, latest upstream HEAD, or third-party tool was
installed. See [evaluation methodology](../metrics/methodology.md).
