# Uninstall

Preview removal from the same checkout and with the same home selection used to install:

```console
dotnet tools/AgentTool.cs uninstall --dry-run
dotnet tools/AgentTool.cs uninstall
```

Uninstall removes only links recorded as toolkit-owned whose current target still
matches. It preserves replacements, unrelated files, parent directories, the toolkit
checkout, project-local templates, `.agent-results/`, and target repositories.

If the checkout was moved, restore it to the recorded path long enough to uninstall or
inspect the reported ownership conflict. Do not delete ambiguous files merely because
their names resemble toolkit components.
