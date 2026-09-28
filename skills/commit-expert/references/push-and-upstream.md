# Push and Upstream Safety

Pushing is a separate repository mutation from creating a commit.

A request to push authorizes the push operation within the requested destination. It does not
authorize new commits, rebases, force-pushes, tag deletion, remote changes, or upstream changes
unless those operations are explicitly included.

## Inspect before pushing

```bash
git remote -v
git branch --show-current
git status --short --branch
git rev-parse --abbrev-ref --symbolic-full-name '@{upstream}' 2>/dev/null || true
```

When a remote is known, inspect its exact URL without exposing embedded credentials in user-facing
output:

```bash
git remote get-url <remote>
```

Do not assume `origin`, `main`, or any provider.

## Confirm the destination

Determine:

- local branch or detached HEAD state
- remote name
- remote branch/ref
- current upstream, if any
- commits that are about to be pushed
- whether the destination is protected or subject to review

For an existing upstream:

```bash
git log --oneline '@{upstream}..HEAD'
git status --short --branch
```

If there is no upstream, do not invent one. Identify the remote and target branch from repository
configuration or explicit user instruction.

## Upstream setup

`git push -u <remote> <branch>` both pushes and changes local tracking configuration.

Only use `-u` or `--set-upstream` when:

- an upstream is already intended by repository/user policy, or
- the user explicitly requested that the branch start tracking that remote branch.

Do not change tracking configuration as a hidden side effect of an ordinary push.

## Push boundaries

Require explicit authorization for:

- force-push
- deleting a remote branch
- pushing all branches
- pushing all tags
- changing a remote URL
- changing fetch/push refspecs
- rewriting public history

A plain push must not be upgraded into any of those operations to work around a rejection.

## Signed commits

If signed commits are required, verify every commit that will be pushed, not just the latest commit.

For a small range this can be inspected with:

```bash
git log --show-signature --oneline '@{upstream}..HEAD'
```

For a new branch without an upstream, determine the exact commit range from the intended base and
verify that range according to repository policy.

See `commit-signing.md`.

## Push failure

If the remote rejects a push:

1. preserve the local commits
2. report the provider's actual error
3. do not force-push automatically
4. do not automatically pull, merge, rebase, or reset
5. explain what repository state is now known

Common non-fast-forward failures require a repository-specific integration decision. That decision
is separate from the original push.

## Verify after push

After success:

```bash
git status --short --branch
git branch -vv
```

Verify that the intended branch and remote-tracking relationship were updated.

If the push was meant to publish a new branch, confirm the configured upstream only when upstream
creation was part of the authorized operation.
