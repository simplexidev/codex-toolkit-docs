# Upstream integrations

The toolkit references official .NET skills and optional diagnostic, compatibility,
security, and release tools through product manifests. Those entries express integration
policy; they are not vendored code, automatic installers, exhaustive version pins, or
verified setup recipes.

`upstream status` reads the recorded policy. `upstream update --dry-run` can report what
would be checked without network access; a real update query uses GitHub CLI and writes a
review artifact under ignored `.agent-tool/`. Drift is reported for human review and is
never automatically merged.

Install third-party skills or tools separately from their current official instructions.
Check the selected version's license and notices before redistribution. The product's
[`upstream/`](https://github.com/simplexidev/codex-toolkit/tree/develop/v2.0.0/upstream)
directory is the canonical recorded policy.
