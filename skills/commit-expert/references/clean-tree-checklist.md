# Working Tree Review Before Finishing

A completion check is about truthful repository state, not about making `git status` look empty.

## Required inspection

Before declaring a repository task complete:

```bash
git status --short --branch
git diff --stat
git branch --show-current
git rev-parse --abbrev-ref HEAD@{upstream} 2>/dev/null || true
```

For machine-readable workflows:

```bash
git status --porcelain=v2 --branch
```

If the status is not clean:

1. distinguish task-owned changes from pre-existing work
2. identify the remaining files and their ownership
3. report whether the changes are staged, unstaged, or untracked
4. commit only after explicit commit authorization
5. leave intentionally uncommitted work in place

A dirty tree is not a failure condition by itself.

## Special states

Check for merge, rebase, cherry-pick, and revert state before declaring a normal task complete:

```bash
git rev-parse -q --verify MERGE_HEAD
git rev-parse -q --verify CHERRY_PICK_HEAD
git rev-parse -q --verify REVERT_HEAD
git rev-parse -q --verify REBASE_HEAD
```

Flag detached HEAD when it is relevant to the requested commit or push.

## Hooks and verification

Before committing:

- inspect repository-declared hooks and checks
- run relevant declared checks within the authorized scope
- report the exact result
- report unavailable checks as skipped
- never claim a check passed without running it

Never bypass hooks with `--no-verify` unless the user explicitly authorizes the bypass. Report any
authorized bypass prominently in the final result.

## Staged and unstaged diff checks

When changes are to be committed:

```bash
git diff --cached --name-status
git diff --cached --stat
git diff --cached --check
```

When working-tree changes remain:

```bash
git diff --name-status
git diff --stat
git diff --check
```

Inspect the full diff when scope, security, or ownership is unclear.

## Secret and sensitive-content check

Before committing, inspect the staged diff for accidental disclosure of:

- API keys
- access tokens
- passwords
- private keys
- credentials
- database connection strings containing secrets
- environment files or values meant to stay local
- secrets copied from logs or error output

A secret scanner provided by the repository can improve coverage, but its absence is not evidence that
the diff is clean.

If a secret is found:

1. do not create or push the commit as though it were safe
2. remove the secret from the staged content when authorized
3. tell the user that replacing a secret in a later commit does not remove it from prior Git objects
4. recommend appropriate credential rotation and history-remediation steps

Do not attempt history rewriting merely because a secret was found.

## Diff size as a caution signal

Use repository-defined size thresholds first.

If none exist, a large diff spanning many files or concerns is a signal to inspect the full patch
and reconsider grouping. Size is not itself a reason to split a coherent change.

## Completion checklist

- [ ] working-tree status inspected
- [ ] current branch identified
- [ ] upstream identified when relevant
- [ ] special Git state checked
- [ ] staged diff inspected when a commit is intended
- [ ] ignore rules checked for new candidate files
- [ ] hooks/checks inspected and relevant checks run
- [ ] secrets reviewed in the staged diff
- [ ] task-owned and pre-existing changes distinguished
- [ ] commit result verified when a commit was created
- [ ] push result verified when a push was performed
- [ ] remaining dirty files reported or intentionally left uncommitted

## Never clean by force

Never use these commands to make the tree look clean unless the user explicitly authorizes the
exact destructive operation and target:

```bash
git restore <file>
git checkout -- <file>
git clean -fd
git reset --hard
```

A clean status produced by deleting user work is not successful task completion.
