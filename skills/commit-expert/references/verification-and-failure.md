# Verification and Failure Handling

Verification matters when external tools, Git state, repository policy, versions, hooks, remotes,
signing environments, or renderers can invalidate an otherwise plausible result.

## Verification vocabulary

Report state using precise categories:

- **not checked**: the condition was not inspected
- **checked and passed**: the relevant command or evidence succeeded
- **checked and failed**: the relevant command or evidence failed
- **skipped**: the check exists or is relevant, but could not or was not authorized to run
- **not applicable**: the condition does not apply to this operation

Do not collapse these into "verified".

## Evidence hierarchy

Prefer, in order:

1. actual command output from the current repository
2. repository-local policy and documentation
3. primary upstream/project documentation
4. static inspection and reasoned inference

When a fact can be cheaply verified, verify the smallest fact that controls the decision instead of
guessing from convention.

## Preconditions

Before a mutation, confirm the conditions that make it safe:

- repository root and current worktree
- intended branch or detached state
- intended remote/upstream when pushing
- current staged scope
- ownership of changes
- relevant policy
- required checks
- signing requirements
- absence of active unexpected Git operations

## Postconditions

After a mutation, verify the result actually exists.

For a commit:

```bash
git log -1 --format=fuller
git status --short --branch
```

For a push:

```bash
git status --short --branch
git branch -vv
```

For signing:

```bash
git log --show-signature -1
```

For the exact message:

```bash
git log -1 --format=%B
```

## Failure classification

Useful failure classes include:

- command unavailable
- permission/authentication failure
- repository not found
- hook rejection
- verification/test failure
- signing failure
- invalid message/policy failure
- unexpected working-tree mutation
- merge/rebase/cherry-pick/revert state
- remote rejection or non-fast-forward
- upstream/destination mismatch

Report the actual class and evidence when possible.

## Failure behavior

When a mutation fails:

1. preserve local work
2. report the actual error
3. re-inspect state before attempting anything else
4. do not broaden the operation
5. do not switch to destructive flags
6. do not silently amend, reset, rebase, or force-push
7. retry only the same non-destructive operation when the failure is clearly transient

After an uncertain failure, assume the side effect may have occurred until the repository state proves
otherwise. Do not blindly rerun a commit or push.

## Verification does not grant permission

A successful dry run, diff, hook check, or local signature verification does not itself authorize
the next mutation.

Inspection answers "what is true?".
Authorization answers "what may be changed?".

Keep them separate.

## Recovery and rollback

After a successful commit or push, verify the intended result.

If something is wrong:

- an unpublished mistaken commit may sometimes be corrected with an explicit amend, reset, revert,
  or follow-up commit depending on the user's intent
- a published mistake should generally be corrected with a new commit unless the user explicitly
  authorizes history rewriting
- a mistaken push to a shared branch must not trigger automatic force-push or history rewrite
- `git reset --hard`, `git push --force`, remote branch deletion, and comparable history/destructive
  operations require explicit, operation-specific authorization

Do not choose a recovery strategy from regret alone. First determine whether the commit is published,
whether others may have consumed it, and what exact outcome the user wants.
