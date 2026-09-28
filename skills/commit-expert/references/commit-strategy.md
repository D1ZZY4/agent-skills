# Commit Strategy

Commit strategy controls how changes are grouped, how messages are formatted, and which optional
metadata is attached. Those are separate dimensions and must not be conflated.

The default grouping strategy is `auto`.

## Resolution order

1. Explicit user instruction for this task.
2. Repository policy or documented repository convention.
3. Portable default: `auto`.

A strategy may not authorize a mutation by itself. Authorization comes from the user request and
the main skill workflow.

## Strategy dimensions

Resolve these independently:

1. Grouping: how changes are divided into commits.
2. Message format: how each commit is written.
3. Metadata: scope, breaking-change markers, trailers, or similar details.

For example, `scope` is message metadata. It is not a reason to split a commit.

## Grouping strategies

| Value | Behavior |
| --- | --- |
| `auto` | Analyze the actual diff. Keep one coherent logical change together. Split independent changes when they can stand alone. Preserve repository conventions. |
| `atomic-commit` | Create one commit per independent logical change. |
| `focused-commit` | Keep all changes required for the same task, issue, or objective together, even across modules. |
| `concern-commit` | Group by independent engineering concern such as auth, database, localization, API, UI, or deployment. |
| `commit-type` | Group clearly separable changes by semantic type such as `feat`, `fix`, `docs`, `test`, or `chore`, without splitting changes that are inherently one logical unit. |

## Message strategies

| Value | Behavior |
| --- | --- |
| `conventional-commit` | Use Conventional Commits syntax such as `type(scope): summary`, with body/footer structure according to repository policy. |

Do not infer a message strategy from a grouping strategy.

## Metadata strategies

| Value | Behavior |
| --- | --- |
| `scope` | Add a meaningful scope when repository policy or user preference calls for it and the affected area can be identified without inventing terminology. |
| `breaking-change` | Mark a compatibility-breaking change with `!` when the convention uses it and explain the break in the message/footer as required by repository policy. |

## Combining values

Grouping, message format, and metadata can be combined:

```text
[atomic-commit, conventional-commit, scope]
```

means:

- split independent logical changes
- use Conventional Commits
- include a meaningful scope when one is justified

Another example:

```text
[focused-commit, conventional-commit]
```

means:

- keep one task or issue together
- use Conventional Commits

Do not treat `scope` or `breaking-change` as grouping instructions.

## The logical-change test

The primary grouping unit is the logical change, not the file, folder, or line count.

A single logical change may span:

- multiple files
- multiple directories
- multiple modules
- implementation and tests
- implementation and required documentation
- configuration and code when the configuration is required for that code to work

Keep changes together when they are causally linked, reviewed together, and would be incomplete or
misleading if separated.

Split changes when they have independent purpose and can be reviewed, reverted, or understood
independently.

## Dependency ordering

When several commits are necessary, prefer an order that keeps each earlier commit valid.

For example:

1. introduce a shared API or schema
2. update consumers
3. update tests or migration follow-up when independently meaningful

Do not force an artificial split when the repository's history convention prefers one coherent change.

## `auto` does not mean arbitrary

`auto` does not:

- force one commit per file
- force one commit per directory
- forbid large commits
- automatically split tests from implementation
- automatically split documentation from implementation
- override explicit user instructions
- override repository policy

A large commit is acceptable when it is cohesive and intentionally one change.

## Signals that a grouping needs reconsideration

Reconsider the grouping when:

- the commit contains unrelated behavior
- it mixes an independent refactor with feature work
- parts can be reverted independently
- parts have different purposes and no dependency
- the message requires repeated "and also" constructions
- one subset would be meaningful on its own

"And also" is a heuristic, not a hard rule.

## Large diffs

Size alone does not define quality.

A large, cohesive change is better represented by one coherent commit than by arbitrary micro-commits.

A large, mixed change should be split when the concerns are independent.

Use repository-defined thresholds first. When none exist, a large multi-file diff is a signal to inspect
more carefully, not permission to rush.
