# AgentTool command reference

Use `dotnet tools/AgentTool.cs help` for the exact command set in your checkout.

| Area | Commands | Purpose |
|---|---|---|
| Lifecycle | `install`, `update`, `uninstall`, `doctor` | Manage owned links and check prerequisites |
| Repository | `repo changed-files`, `locate`, `health`, `affected-projects` | Compute scoped repository facts |
| Git/GitHub | Git state, commit/issue/PR preparation, review comments | Inspect or safely prepare workflows without publishing |
| .NET | `verify`, `format`, `package-audit`, `api-check`, `release-verify` | Targeted validation and explicit gates |
| Evidence | `logs summarize`, `sarif summarize` | Bound large diagnostic output |
| Judgment | `jev noul`, `choice`, `score`, `screen`, `cache-clear` | Optional bounded semantic classification |
| Upstreams | `upstream status`, `update --dry-run` | Report integration policy and drift |
| Product | `validate`, `eval`, `release` | Validate metadata/evals and package a release |
| Results | `results init`, `new`, `list`, `latest`, `context`, `clean` | Manage durable cross-session evidence |

Common options include `--root DIR`, `--toolkit DIR`, `--json`, and `--help`. Exit code 0
means success; command failures use nonzero status, and required-mode JEV service failure
uses 3 while returning `REVIEW` semantics.

AgentTool passes argument arrays without a shell and bounds child execution. It does not
commit, push, merge, install third-party tools, or pull updates. Some commands can still
run builds, MSBuild evaluation, GitHub CLI, or package audit, so review the target and
network implications before invoking them.
