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

## Recovery and rollback

After a successful commit or push, verify the intended result. If something is wrong:

- A mistaken commit on the current branch can be amended or reverted with an additional commit.
- A mistaken push to a shared branch requires explicit authorization before rewriting history.
- `git reset --hard`, `git push --force`, and history rewriting are destructive. Never run them
  without explicit, specific user instruction.

When the user reports regret after a mutation, stop and ask before running further destructive
commands. Do not assume a recovery strategy; Git offers multiple paths and choosing the wrong
one can make the situation worse.
