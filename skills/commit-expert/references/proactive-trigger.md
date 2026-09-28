# Proactive Trigger

Use this reference when the agent has finished real work and the user did not explicitly request a
commit.

The goal is one useful check-in, not a running Git conversation.

## When to act

- After the agent creates or edits repository files and the working tree contains new task-owned
  changes, inspect `git status --short` before ending the turn.
- Before declaring the task complete, inspect the tree when the task involved repository changes.
- If the user explicitly asked to commit or stage, skip this check-in and enter the normal
  workflow.
- If the user explicitly asked to push, inspect push state, then follow `push-and-upstream.md`.

## When to stay quiet

- The tree is clean.
- The dirty state is caused only by clearly pre-existing work the user never claimed.
- The same task-owned diff was already offered for commit and the user declined. Do not ask again
  unless new task-owned changes appear.
- The user asked a narrow question that happened to touch a file. Reading a file is not authoring
  a change.

## Confidence rule

A dirty tree is not enough to trigger a commit prompt. Ownership must be established first.

Distinguish:

- changes created by this task
- changes that predate this task
- changes with unclear provenance

Unclear provenance is not permission to offer the whole tree. If task-owned changes are mixed with
pre-existing ones, report the distinction and propose only the task-owned scope.

## How to offer

Ask once:

> Need to commit these changes?

Supported responses are:

- yes
- no
- a specific instruction such as "commit docs only", "split by package", or "not yet"

Routing:

- `no`: do not touch Git. Do not ask again unless new task-owned changes appear.
- `yes`: continue with the normal commit workflow. Do not ask for extra explanation when the diff
  clearly explains the change.
- custom instruction: follow the actual instruction and resolve scope before mutation.

Only request extra context when the diff cannot explain an important part of the message, such as a
business reason, an issue reference, an intentional compatibility decision, or a migration rationale.

A clean tree means silence. A dirty tree after real work means one short check-in, then stop and
follow the user's answer. Do not repeat the same prompt merely because the user continues unrelated
work without changing the task-owned diff.
