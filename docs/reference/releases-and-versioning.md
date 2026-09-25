# Releases and versioning

Use a reviewed GitHub release or tag for repeatable installation. The `develop/v2.0.0`
branch is a development line, not proof that v2 has shipped. Consult the product's
[`releases`](https://github.com/simplexidev/sdeveng/releases) and
[`CHANGELOG.md`](https://github.com/simplexidev/sdeveng/blob/develop/v2.0.0/CHANGELOG.md)
for the actual published history.

Product versions are synchronized across `config/toolkit.json` and both plugin manifest
copies. Release validation runs tests, metadata validation, offline scenario checks, and
format/diff checks. The release workflow packages reviewed source and configuration and
publishes a SHA-256 checksum; tests, caches, and local result stores are not release
payloads.

The project template's `version.json` is only a starting point for repositories that
choose Nerdbank.GitVersioning. The `versioning` skill applies an existing policy; it does
not invent one or publish a release without authorization.
