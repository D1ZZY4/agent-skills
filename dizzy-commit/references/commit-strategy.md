# Commit Strategy

Strategy controls how the agent groups changes into commits and shapes commit messages. The
default is `auto`. Repository policy or the user can override it, and the user can state a
one-off strategy for a single task.

## Resolution order

1. Explicit user instruction for this commit.
2. Repository policy: the `strategy` field in the policy shape, or a documented repository
   convention.
3. Default: `auto`.

## Values

| Value | What the agent does |
|---|---|
| `auto` | Analyze the working set and pick the most sensible grouping and message format. Prefer one logical change per commit, follow repository conventions when present, and do not split a single coherent change by file count alone. |
| `conventional-commit` | Format every message as `type(scope): summary`, with a body when the change is non-trivial. |
| `atomic-commit` | One commit per logical change. Split distinct concerns into separate commits. |
| `focused-commit` | One commit per task or issue. Keep all files for that task together, even across modules. |
| `commit-type` | Group the working-set changes by type (feat, fix, docs, chore, and so on) and make one commit per group. |
| `scope` | Apply a meaningful, non-fabricated scope inside `type(scope)`. |
| `breaking-change` | Mark breaking commits with `!` after the type and add `BREAKING CHANGE:` to the body. |
| `concern-commit` | Group by concern dimension: feature, bug fix, docs, dependency, or config. |

Values can combine. For example, `[conventional-commit, scope]` means conventional format with
a meaningful scope, while `[atomic-commit, concern-commit]` means one commit per concern
dimension. `auto` is the standalone default; pairing other values with it uses them as the
preferred levers inside auto mode.

## What auto does not do

- Auto does not ban large commits. A big commit that is one coherent change is fine.
- Auto does not force one commit per file. Grouping follows logical change, not file count.
- Auto does not override an explicit user instruction. When the user says "commit everything
  as one" or "split by folder," follow that instruction.

## Sign of a weak grouping

If writing the message requires "and also" to describe the change set, the commit probably
holds more than one logical change, and splitting is worth proposing. This is a signal, not a
hard ban: the user decides whether to accept the split or keep one commit.