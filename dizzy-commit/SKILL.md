---
name: dizzy-commit
description: >
  Guide safe, repository-aware Git commits and pushes. Inspect repository policy, working-tree
  state, diffs, hooks, tests, branch/upstream configuration, and commit conventions before any
  mutation. Never commit, push, stage, restore, or discard changes without explicit authorization
  for that side effect. Use Conventional Commits only when repository policy or the user requires it.
license: MIT
metadata:
  version: 1.10.0
  author: D1ZZY4
  priority: high
---

# Dizzy Commit

This skill is a safety workflow, not permission to modify the repository.

## Policy precedence

Read `references/policy-configuration.md`. Resolve rules in this order:

1. Platform and system safety constraints.
2. Repository policy and contribution instructions.
3. Explicit user instructions.
4. This skill's portable defaults.

Never invent branch names, scopes, authorship, remotes, commit formats, or required checks.

## Safety boundary

Inspection is safe by default. Mutation is not.

Without explicit authorization, do not:

- stage or unstage files,
- create or amend commits,
- push or force-push,
- restore or delete files,
- clean untracked files,
- rewrite history,
- change Git configuration.

Treat pre-existing changes as user-owned unless provenance is clear.

## Step 0: Establish intent and mode

Determine whether the user wants inspection, preparation, commit creation, push, or the full
sequence. If the request authorizes only one side effect, do not silently perform the next one.

Read `references/host-adapters.md` when the environment is not ordinary Git CLI usage.

## Step 1: Inspect before deciding

At minimum, inspect status and the relevant diff. Check branch/upstream information and repository
policy when committing or pushing. Identify generated files, secrets, unrelated changes, merge
conflicts, and staged-versus-unstaged differences.

Read `references/clean-tree-checklist.md` and `references/staging-and-gitignore.md`.

## Step 2: Scope the change

Separate task-related changes from pre-existing or unrelated work. Never stage "everything"
merely because it is convenient. Prefer explicit paths and verify the staged diff before commit.

## Step 3: Determine the commit message

Read `references/message-style.md`. Use repository conventions if present. Conventional Commits
is a fallback, not a universal law. The subject should describe the resulting change, not the
agent's process.

## Step 4: Verify

Run the repository's documented checks when authorized and relevant. If checks are unavailable,
say so. Never claim tests passed when only static inspection occurred.

Before a commit, verify the staged diff and intended paths. Before a push, verify the commit,
remote, branch, and upstream relationship.

## Step 5: Mutate only within the granted scope

After explicit authorization, stage exactly the intended paths, create the commit, and verify the
result. Pushing requires explicit push authorization unless the user clearly requested a push.

## Anti-patterns

- `git add .` without reviewing scope.
- Cleaning a dirty tree to make a task easier.
- Amending or force-pushing without explicit instruction.
- Hiding unrelated changes in a commit.
- Claiming hooks/tests passed without evidence.
- Changing Git config to satisfy a local policy.
- Treating a dirty working tree as an error that must be "fixed".
- Using em dashes in commit messages.

## Caveman mode

If the user explicitly asks for a direct commit and the repository is straightforward, still perform
the minimum safety checks. Direct intent is authorization to mutate, not authorization to skip review.

## Bundled references

Load the specific policy, staging, message, verification, and push references required by the task:

- `references/policy-configuration.md`: policy precedence order and what never to invent.
- `references/host-adapters.md`: when the environment is not ordinary Git CLI usage and how to
  adapt.
- `references/clean-tree-checklist.md`: what to inspect before deciding to commit.
- `references/staging-and-gitignore.md`: group by logical concern, never cite ignored files, never
  add new ignored files, verify gitignore status before staging.
- `references/message-style.md`: commit message format, subject rules, body rules, prohibited
  content, AI co-author trailer, and type reference.
- `references/commit-execution.md`: duplicate-commit check, subject/body structure, avoiding literal
  `\n` in shell, two `-m` flags versus file plus `-F`, and post-commit verification.
- `references/proactive-trigger.md`: when to check in without an explicit commit request and the
  check-in flow.
- `references/strict-mode.md`: extra constraints for strict mode, applied on top of default rules.
- `references/push-and-upstream.md`: push authorization, upstream verification, and when to update
  the branch.
- `references/examples.md`: worked good/bad commit message examples.
- `references/verification-and-failure.md`: shared verification and failure-handling principles.
