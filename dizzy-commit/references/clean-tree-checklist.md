# Working Tree Review Before Finishing

Before declaring any task complete or ending a session, inspect the working tree:

```bash
git status --short
```

If the output is not empty:

1. Distinguish changes made during this task from pre-existing user work.
2. Report the remaining files and their ownership.
3. Commit only after explicit user approval, or leave the changes in place when the user
   intentionally wants them uncommitted.
4. Never use `git checkout -- <file>` or `git clean -fd` to force a clean tree. Destructive
   cleanup requires explicit, file-specific confirmation.

## Checklist before done

- [ ] `git status --short` was inspected
- [ ] `git diff --stat` was inspected when changes exist
- [ ] `git diff --cached --stat` was inspected when staged changes exist
- [ ] Remaining changes were reported or explicitly approved for commit
- [ ] Any remaining dirty files are pre-existing user work or were explicitly kept

## Secret and sensitive content check

Before committing, scan the staged diff for:

- API keys, tokens, passwords, private keys, credentials
- Environment variables that should remain local
- Database connection strings with embedded credentials
- Third-party secrets copied from logs or error output

If found, remove the secret from the diff before committing. Replacing a secret with a placeholder in committed history does not remove it from Git's object database; in that case, advise the user separately and do not treat the commit as safe until they handle the history.

## Diff size threshold

Treat large diffs as a signal to slow down, not as permission to speed up. A diff exceeding roughly 500 lines changed across 10 or more files usually indicates mixed concerns. In that case:

1. Inspect the full diff before committing.
2. Ask whether the change should be split into multiple commits.
3. Do not combine unrelated changes into one commit unless the user explicitly approves the combined scope after seeing the diff.
