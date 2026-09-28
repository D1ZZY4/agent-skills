# Worked Examples

These examples illustrate the workflow, not a universal commit style. Repository policy always wins.

## 1. Good default mode

```text
feat(api): add GET /users/:id/profile

Add a dedicated profile endpoint so mobile clients can request
profile data without the full user payload.

Closes #128
```

Why it works:

- describes the resulting change
- explains the reason
- keeps the issue reference in the footer area
- contains no fabricated process narration

## 2. Good strict mode

```text
fix(button): restore dark mode danger contrast

Use the existing danger-state tokens so the dark variant keeps the
same semantic meaning as the light variant.
```

Strict mode is concerned with policy compliance, staged scope, checks,
author, and signing. It does not require a different semantic grouping.

## 3. Good atomic split

Two independent changes:

```text
fix(cache): invalidate stale profile entries
```

```text
docs(api): document profile cache behavior
```

Do not combine them simply because both touch the same feature area.

## 4. Good coherent multi-file commit

A single feature spans:

```text
apps/api/profile.ts
apps/api/profile.test.ts
docs/api-profile.md
```

If all three are required for the same feature and were changed together intentionally, keeping them
in one commit is valid.

## 5. Good focused task commit

A migration task changes schema, worker code, tests, and migration documentation.

When all pieces are required for the same migration, one focused commit can be appropriate:

```text
feat(storage): migrate job records to versioned schema
```

Do not split the migration solely because it crosses four directories.

## 6. Bad bundled commit

```text
refactor: clean up repository changes

- fix auth redirect
- update database indexes
- reformat UI
- remove old docs
- bump unrelated packages
```

If these changes are independent, split them.

## 7. Bad generic message

```text
chore: update files
```

This communicates almost nothing about the resulting diff.

Prefer the actual behavior or maintenance reason.

## 8. Bad process narration

```text
fix(api): changes after running tests
```

The tests are verification evidence, not the reason for the change.

## 9. Multi-line body using `-m`

```bash
git commit   -m "fix(auth): reject expired refresh tokens"   -m "Reject expired tokens before session lookup.

- Preserve the existing valid-token path
- Keep the established error contract"
```

Do not put a literal `\n` sequence into a shell argument and assume it is a line break.

## 10. Multi-line body using a message file

Message file:

```text
docs(api): document versioned profile responses

Document the response versions and the migration path.

- Explain the new field
- Explain compatibility with the previous response

Refs #421
```

Commit:

```bash
git commit -F <message-file>
```

## 11. Good staged-scope check

Before commit:

```bash
git diff --cached --name-status
git diff --cached --stat
git diff --cached --check
```

If the output contains an unrelated file, do not silently unstage or delete it. Re-scope the index
within the authorized operation.

## 12. Pre-existing user work

Status:

```text
 M src/feature.ts
 M notes/local-work.md
?? tmp/debug.log
```

If the task only changed `src/feature.ts`, the agent must not stage the notes or log.

The clean result may intentionally remain:

```text
 M notes/local-work.md
?? tmp/debug.log
```

That is not a failure.

## 13. New ignored file

Status does not show:

```text
.env.local
```

But:

```bash
git check-ignore -v -- .env.local
```

reports that it is ignored.

Do not force-add it. Treat the ignore rule as intentional unless the user explicitly names and
authorizes that specific file.

## 14. Ignored local policy citation

Bad:

```text
docs(repo): update references

Per local-prompt.md, remove the generated guide.
```

when `local-prompt.md` is ignored.

Better:

```text
docs(repo): update references

Remove the generated guide from the tracked reference index because
the release workflow regenerates it.
```

## 15. No upstream configured

Inspection:

```text
git rev-parse --abbrev-ref --symbolic-full-name '@{upstream}'
fatal: no upstream configured for branch 'feature/profile'
```

Do not assume `origin/feature/profile`.

Report the missing upstream and use the remote/branch explicitly identified by the user or repository
workflow. Creating tracking configuration requires its own authorization.

## 16. Push rejection

A push returns:

```text
! [rejected] feature/profile -> feature/profile (non-fast-forward)
```

Correct behavior:

- keep the local commits
- report the rejection
- do not force-push
- do not automatically rebase or reset
- wait for the repository/user's integration decision

## 17. Signed commit verification

Before push:

```bash
git log --show-signature -1
```

If verification reports a bad or missing signature under a policy that requires signing, do not pretend
the commit is verified.

Do not change the signing key merely to make the check pass.

## 18. Hook rejection

A `commit-msg` or `pre-commit` hook fails.

Correct behavior:

- preserve the staged diff
- report the hook failure
- inspect the repository's expected fix
- do not use `--no-verify` automatically

## 19. Merge or rebase in progress

If Git reports an active merge or rebase state, do not write an ordinary feature/fix commit on top
of it without understanding what operation is already in progress.

Follow the existing operation's rules.

## 20. Direct commit request

User says:

```text
commit these changes
```

This authorizes the commit workflow for the intended task scope.

It does not authorize:

- pushing
- force-pushing
- changing Git identity
- changing signing keys
- deleting unrelated work

## 21. Commit and push request

User says:

```text
commit these changes and push the branch
```

This authorizes both operations, subject to repository policy and the normal verification gates.

If the branch has no upstream, determine the required destination. Do not silently add `-u` unless the
request or repository policy also authorizes creating tracking configuration.

## 22. Good breaking change

```text
feat(api)!: rename profile response field

Clients must migrate from `displayName` to `name` before the old
field is removed.

BREAKING CHANGE: `displayName` is no longer returned by the profile
endpoint.
```

The body explains consumer impact rather than merely announcing that the change is breaking.

## 23. Bad "changelog dump"

```text
feat(api): update profile

- modified profile.ts
- modified profile.test.ts
- modified README.md
- modified types.ts
- modified route.ts
```

The commit body should summarize the engineering change, not reproduce the file list.

## 24. Bad forced cleanup

Working tree:

```text
 M src/feature.ts
 M notes/todo.md
```

Bad response:

```bash
git restore notes/todo.md
git clean -fd
```

The goal of the skill is not a pretty status output. Preserve user work.

## 25. Verify the final commit

After commit:

```bash
git log -1 --format=fuller
git log -1 --format=%B
git status --short --branch
```

Do not report "committed successfully" from the exit code alone without checking the resulting state.
