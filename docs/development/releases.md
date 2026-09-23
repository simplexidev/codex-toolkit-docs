# Prepare a release

Release work is product-owned and authorization-sensitive.

1. Run the full test suite, AgentTool metadata validation, offline scenario checks, and
   `git diff --check`.
2. Verify plugin manifests and `config/toolkit.json` use the same semantic version.
3. Review security, third-party notices, changelog, schemas, and packaged contents.
4. Create and push `vMAJOR.MINOR.PATCH` only when authorized.
5. Inspect the draft GitHub release and SHA-256 checksum before publication.

The source archive includes the runtime source and configuration users need, not tests,
caches, local prompts, private metrics, or developer result stores. CodeQL is a separate
gate where repository code scanning is available.

API compatibility, SBOM, reproducibility, and specialized project gates remain explicit,
on-demand checks unless the product policy says otherwise. Do not represent an incomplete
gate as release approval.
