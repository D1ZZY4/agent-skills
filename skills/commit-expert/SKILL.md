---
name: commit-expert
description: >
  Guide safe, repository-aware Git commits and pushes. Inspect repository policy, working-tree
  state, diffs, hooks, tests, branch/upstream configuration, signing, and commit conventions
  before mutation. Never stage, commit, push, restore, delete, clean, or rewrite history without
  the authorization required for that specific side effect. Use Conventional Commits only when
  repository policy or the user requires it.
license: SSPL-1.0
metadata:
  version: 1.18.0
  author: D1ZZY4
  priority: high
---

# Commit Expert

## Purpose

This skill is a safety workflow, not permission to modify a repository.

The agent must inspect the repository and the actual working state before any Git mutation.
It must preserve unrelated work, respect repository policy, and report verification results from
evidence rather than inference.

A clean tree is a valid outcome. A dirty tree is not a problem that must be "fixed".

## Core principles

1. Inspection is safe by default. Mutation is not.
2. Authorization is operation-specific. Committing does not silently authorize pushing, and pushing
   does not silently authorize committing.
3. Treat pre-existing or unowned changes as user-owned until their provenance is clear.
4. Repository policy beats portable defaults. Explicit user preferences can override style defaults,
   but do not override higher-priority safety constraints or mandatory repository policy.
5. Never invent branch names, remotes, upstreams, authors, emails, signing keys, scopes, commit
   conventions, required checks, or successful results.
6. Derive the commit message from the actual diff and resolved policy, not from a task plan.
7. Verify both preconditions and postconditions around every mutation.
8. Never use destructive Git commands to make the repository easier to reason about.

## Authorization model

Interpret authorization narrowly:

| User instruction | Authorized side effects |
| --- | --- |
| "inspect/check/review" | Read-only inspection |
| "stage/add these files" | Stage only the named or clearly identified paths |
| "commit these changes" | Stage the intended task changes as necessary, create the commit, verify it |
| "push these commits" | Inspect and push the intended existing commits; do not create a new commit |
| "commit and push" | Commit workflow plus push workflow, including separate verification |
| "amend/reword/squash/rebase/reset/restore/clean" | Only the specifically requested operation |
| "force-push/delete remote branch/change remote/configure signing" | Only that exact operation, after confirming the target and consequences |

Creating or changing upstream tracking configuration is itself a repository-state mutation. Do not
add `-u` or `--set-upstream` merely because a push command would otherwise fail.

"Commit" authorizes staging only to the extent required to construct the intended commit. It does
not authorize staging unrelated files, ignored files, or pre-existing work.

## Priority and policy resolution

Read `references/policy-configuration.md` before committing or pushing.

Resolve rules in this order:

1. Platform, system, and tool safety constraints.
2. Repository policy and contribution documentation.
3. Explicit user instructions and preferences.
4. Portable defaults in this skill and its references.

When two applicable sources conflict, apply the higher-priority source and report the conflict when
it changes the operation or message.

## Step 0: Establish scope and repository state

Determine whether the user wants inspection, preparation, commit creation, push, or a full sequence.
Do not silently advance to another side effect.

Locate the repository root and inspect the working state:

```bash
git rev-parse --show-toplevel
git status --short --branch
git branch --show-current
git rev-parse --abbrev-ref --symbolic-full-name '@{upstream}' 2>/dev/null || true
```

Use `git status --porcelain=v2 --branch` when machine-readable, stable output is useful.

Also detect special Git states before creating an ordinary commit:

```bash
git rev-parse -q --verify MERGE_HEAD
git rev-parse -q --verify CHERRY_PICK_HEAD
git rev-parse -q --verify REVERT_HEAD
git rev-parse -q --verify REBASE_HEAD
```

A merge, cherry-pick, revert, or rebase in progress changes the meaning of the next commit. Do not
turn such a state into an ordinary task commit without understanding and preserving that operation.

Read the relevant references listed at the end of this file. Do not load every reference blindly when
the task only needs a subset, unless strict mode or repository policy requires the full set.

## Step 1: Inspect before deciding

At minimum, inspect:

- working-tree status
- staged and unstaged diffs
- current branch and upstream
- repository contribution/policy guidance
- hooks and relevant verification commands
- secrets and generated files
- task ownership versus pre-existing work
- ignore rules for candidate files

Use:

```bash
git status --short --branch
git diff --stat
git diff --cached --stat
git diff --name-status
git diff --cached --name-status
```

When scope is unclear, inspect the actual diff before asking for or exercising mutation authority.

## Step 2: Resolve policy and commit strategy

Read `references/policy-configuration.md`.

Resolve the grouping strategy from `references/commit-strategy.md`, then resolve the message format
from `references/message-style.md`.

The primary grouping unit is the logical change. File count, directory boundaries, or line count
alone do not define a commit boundary.

## Step 3: Stage only the intended scope

Read `references/staging-and-gitignore.md`.

After explicit authorization, stage exact paths that belong to the resolved commit. Prefer explicit
pathspecs over broad commands.

Never stage an ignored new file with `git add -f` unless the user explicitly identifies and authorizes
that file.

Before committing, inspect:

```bash
git diff --cached --name-status
git diff --cached --stat
git diff --cached --check
```

The staged diff is the source of truth for what the commit will contain.

## Step 4: Verify before commit

Read `references/clean-tree-checklist.md` and `references/verification-and-failure.md`.

Run repository-declared checks when they are relevant and when the user has authorized the commit
workflow. If a required check is unavailable, report it as skipped. Never convert "not run" into
"passed".

Do not bypass hooks with `--no-verify` unless explicitly authorized. If hooks fail, preserve the
failure and report the hook output rather than bypassing it automatically.

## Step 5: Construct the message

Read `references/message-style.md` and `references/commit-execution.md`.

The subject must describe the resulting change. The body must explain why when policy or complexity
requires it. Breaking changes, security fixes, migrations, and reverts require sufficient context.

Do not mention agent involvement in the subject or body. A valid provider-issued `Co-authored-by`
trailer is the only permitted location when repository policy or the user wants that attribution.

## Step 6: Create and verify the commit

Read `references/commit-execution.md` and, when applicable, `references/commit-signing.md`.

Before mutation, perform the duplicate-commit check and re-check the staged diff.

After the commit:

```bash
git log -1 --format=fuller
git status --short --branch
```

Verify that the expected commit exists, the message structure is correct, the author is correct,
and required signing is valid.

Do not amend a pushed commit to repair style or metadata unless the user explicitly requests a
history rewrite and understands the target.

## Step 7: Push only within explicit scope

Read `references/push-and-upstream.md` whenever push is in scope.

Confirm:

- current branch
- exact remote
- exact destination branch/ref
- upstream relationship
- commits that will be pushed
- required checks and signatures
- absence of unintended staged or unstaged changes

Pushing is a separate mutation. Do not infer it from a commit request.

After a successful push, verify local status and branch/upstream state.

## Failure handling

Read `references/verification-and-failure.md`.

When any command fails:

- report the actual failure
- preserve local work
- do not silently broaden scope
- do not substitute a destructive command
- do not claim success from partial output
- retry only when the same non-destructive operation is clearly safe and the failure is transient

For push rejection, do not automatically pull, rebase, merge, or force-push. First explain the
remote rejection and preserve the local commits.

## Anti-patterns

- `git add .` or `git add -A` without a reviewed, intentionally whole-repo scope
- cleaning a dirty tree to simplify the task
- assuming `origin` or `main`
- assuming the branch has an upstream
- changing identity, signing, credentials, remotes, or global Git config to satisfy a local rule
- staging ignored files because they are convenient
- hiding unrelated changes inside the requested commit
- committing during a merge/rebase/cherry-pick/revert without understanding the operation
- using `--no-verify` to make a failing commit pass
- amending or force-pushing public history without operation-specific authorization
- claiming hooks, tests, signatures, or pushes succeeded without evidence
- using em dash characters in commit messages

## Direct or "caveman" mode

A direct mutation request is authorization to mutate only within the requested scope. It is not
authorization to skip inspection, policy resolution, diff review, or verification.

Even for "just commit this", perform the minimum safe checks before staging and committing.

## Bundled references

- `references/policy-configuration.md`: precedence, repository policy discovery, and portable defaults.
- `references/commit-strategy.md`: grouping, message format, metadata, and strategy resolution.
- `references/host-adapters.md`: hosting/provider-specific behavior without hard-coding a provider.
- `references/clean-tree-checklist.md`: working-tree, hook, secret, diff, and completion checks.
- `references/staging-and-gitignore.md`: staging scope, ownership, ignored files, and index review.
- `references/message-style.md`: subject, body, trailer, punctuation, and commit type rules.
- `references/commit-execution.md`: commit construction, shell-safe message handling, hooks, and
  post-commit verification.
- `references/commit-signing.md`: signing policy, signing mechanics, and signature verification.
- `references/proactive-trigger.md`: when to ask about a commit without being explicitly prompted.
- `references/strict-mode.md`: stricter validation layered on top of the default workflow.
- `references/push-and-upstream.md`: destination verification, push authorization, and upstream safety.
- `references/examples.md`: worked examples for normal, strict, failed, and partial workflows.
- `references/verification-and-failure.md`: shared evidence, failure, and recovery rules.
