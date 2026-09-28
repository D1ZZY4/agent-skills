# Commit Execution Mechanics

This reference covers the mechanics of creating a commit after scope, policy, staging, and
verification have already been resolved.

## Re-check before committing

A long-running agent session can change the repository between inspection and mutation.

Immediately before the commit command:

```bash
git status --short --branch
git diff --cached --name-status
git diff --cached --stat
git diff --cached --check
git log --oneline -5
```

If the staged state changed unexpectedly, stop and re-scope it.

## Duplicate-commit check

Do not create a duplicate commit simply because the workflow resumed.

If a recent commit has essentially the same subject and affected file set as the intended change:

1. inspect `git status`
2. inspect recent history
3. determine whether the earlier commit already completed the task
4. create another commit only when real uncommitted work remains

Do not compare only the subject. The actual staged diff is authoritative.

## Special repository states

Before creating an ordinary commit, check for active operations such as merge, cherry-pick, revert,
or rebase.

A commit that finalizes one of those operations is not equivalent to an ordinary task commit. Follow
the existing operation and repository guidance rather than replacing it with a new message strategy.

## Commit message structure

A message with a body has this shape:

```text
subject

body

trailers-or-footers
```

There must be a real blank line between subject and body.

Do not assume that typing the characters `
` into a shell string creates a newline. Shell behavior
differs, and literal escape text is easy to introduce by accident.

## Method 1: multiple `-m` blocks

For a short body:

```bash
git commit -m "type(scope): summary" -m "Why the change exists.

- Related reason
- Important constraint"
```

Each `-m` argument supplies a separate paragraph.

## Method 2: message file with `-F`

For multi-line bodies, bullets, breaking changes, or trailers, prefer a message file:

```text
<message-file>

type(scope): summary

Why the change exists.

- Related reason
- Important constraint

Refs #123
```

Then:

```bash
git commit -F <message-file>
```

Create and remove the temporary file using the host environment's native file-writing and cleanup
mechanism. Do not assume Bash syntax when the host shell is different.

## Hooks are part of execution

Git may run `pre-commit`, `prepare-commit-msg`, `commit-msg`, and post-commit/rewrite hooks.

Hooks can:

- modify the message
- reject the commit
- add or normalize trailers
- run formatters or checks

Do not bypass hooks with `--no-verify` unless explicitly authorized.

If a hook fails, preserve the error and fix the underlying issue or obtain a specific authorization
for an exception.

## Verify the resulting commit

After success:

```bash
git log -1 --format=fuller
git status --short --branch
```

Also verify:

- the subject and body are separated correctly
- required trailers are present
- no literal `\n` text was introduced
- the author/committer match the resolved policy
- required signing is valid
- the expected changes are in the new commit
- unrelated working-tree changes remain untouched

For precise message inspection:

```bash
git log -1 --format=%B
```

## Author identity

In strict mode, resolve the author before committing and verify the resulting commit:

```bash
git log -1 --format="%an <%ae>"
```

Also remember that author and committer identity are distinct Git fields. If a repository uses a
non-default environment, inspect both when policy cares about them.

## Amendments

Amending is history rewriting.

Only amend an unpublished commit when the user has authorized the amendment or the normal workflow
explicitly requires it.

Do not amend a commit already pushed to the configured upstream unless the user explicitly instructs
the history rewrite.
