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

## Research-specific verification

- Read the full scope before judging any of it. Unfamiliar is not the same as wrong;
  check the cited source before calling a claim incorrect.
- When project conventions and this skill's defaults conflict, project conventions win.
- Confirm quoted versions, URLs, and command shapes against a fetched source, not
  against another sentence in the same draft.
- State plainly what was not checked (sampled URLs, untested commands, paywalled
  sources) instead of implying full coverage.
