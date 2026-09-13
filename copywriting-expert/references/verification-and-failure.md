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

## Copywork-specific verification

- Read the project's existing strings before claiming a house term or established voice is
  wrong. Unfamiliar is not the same as wrong.
- Confirm terminology against the project's approved glossary first, then the language
  authority, in that order. See `language-and-vocabulary-verification.md`.
- When project conventions and this skill's defaults conflict, project conventions win. Note
  the resolution if a reviewer will wonder why a default was overridden.
- For high-stakes copy, verify the claims it makes against the product's actual behavior or
  documented capabilities. Never assert a promise the product does not make.
- State plainly when copy was not verified instead of presenting it as final.
