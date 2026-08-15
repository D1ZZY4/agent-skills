# Verification and Failure Handling

For tasks that depend on external tools, versions, renderers, repository state, or other facts
that can invalidate an otherwise plausible answer.

## Rules

- Verify the smallest fact that controls the decision.
- Prefer primary, project-local, and version-matched sources.
- Distinguish "not checked", "checked and passed", and "checked and failed".
- If a dependency or tool is unavailable, continue with a safe static workflow when possible.
- Never invent successful execution, compatibility, test results, or installed tools.
- Record assumptions when they materially affect the output.
- If verification would cause a side effect, obtain the required authorization first.
