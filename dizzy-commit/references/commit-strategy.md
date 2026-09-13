# Commit Strategy

Commit strategy controls how the agent groups changes into commits and constructs commit
messages. The default is `auto`.

Repository policy or explicit user instructions can override the default. A user may also
specify a one-off strategy for a single task.

## Resolution order

1. Explicit user instruction for this task.
2. Repository policy: the `strategy` field in the repository policy, or a documented repository
   convention.
3. Default: `auto`.

## Strategy dimensions

Commit behavior has three separate dimensions:

1. Grouping: how changes are divided into commits.
2. Message format: how commit messages are written.
3. Metadata: additional information such as scope or breaking-change markers.

Do not treat message format or metadata as grouping rules unless explicitly requested.

## Grouping strategies

| Value            | What the agent does                                                                                                                                                                                                         |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `auto`           | Analyze the working set and choose the most sensible grouping. Prefer one logical change per commit, preserve repository conventions, and do not split a coherent change merely because it spans multiple files or modules. |
| `atomic-commit`  | Create one commit per logical change. Separate distinct changes when they can stand independently.                                                                                                                          |
| `focused-commit` | Keep all changes belonging to the same task or issue together, even when they span multiple modules. Do not split them merely because they affect different files.                                                          |
| `concern-commit` | Group changes by distinct engineering concerns such as authentication, moderation, database, localization, UI, API, or deployment. Split unrelated concerns when they can be committed independently.                       |
| `commit-type`    | Group clearly separable changes by change type such as `feat`, `fix`, `docs`, `test`, or `chore`. Do not force a split when different types are inherently part of the same logical change.                                 |

## Message strategies

| Value                 | What the agent does                                                                                                                             |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `conventional-commit` | Format each commit message using Conventional Commits, such as `type(scope): summary`. Add a body when useful or required by repository policy. |

## Message metadata

| Value             | What the agent does                                                                                                                                                                                                                       |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `scope`           | Add a meaningful scope to Conventional Commit messages when the affected subsystem can be identified without inventing a scope.                                                                                                           |
| `breaking-change` | Mark a commit as breaking when it changes an established interface or behavior in a way that can break consumers. Use `!` after the type and document the change with a `BREAKING CHANGE:` footer when required by repository convention. |

## Combining values

Grouping, message format, and metadata can be combined.

For example:

```text
[atomic-commit, conventional-commit, scope]
```

means:

* split changes into atomic logical commits
* use Conventional Commits
* include a meaningful scope

Another example:

```text
[concern-commit, conventional-commit, scope]
```

means:

* group independent changes by engineering concern
* use Conventional Commits
* include a meaningful scope

`auto` is the standalone default. Other values may be used as explicit preferences inside
auto mode when the repository policy or user instruction allows them.

Do not interpret `scope` or `breaking-change` as instructions to split commits.

## Grouping principles

The primary unit of grouping is the **logical change**, not the file, directory, or line count.

A single logical change may legitimately span:

* multiple files
* multiple directories
* multiple modules
* implementation and tests
* implementation and required documentation

Do not create separate commits solely because those changes live in different files or modules.

Conversely, changes should be split when they represent independent concerns, behaviors, or purposes
and can be reviewed, reverted, or understood independently.

## What `auto` does not do

* `auto` does not ban large commits. A large commit is acceptable when it represents one coherent
  logical change.
* `auto` does not force one commit per file.
* `auto` does not force one commit per directory.
* `auto` does not automatically split tests, documentation, or configuration from an implementation
  change when they are required parts of the same logical change.
* `auto` does not override an explicit user instruction.
* `auto` should preserve existing repository commit conventions when they are clear and consistent.

Examples of explicit user instructions:

```text
commit everything as one
split independent changes into separate commits
keep this feature in one commit
split commits by concern
```

Follow the user's instruction for the current task unless it conflicts with repository policy or a
higher-priority requirement.

## Signals of weak grouping

A grouping may be worth reconsidering when:

* the commit contains unrelated behavioral changes
* the commit mixes independent refactors with feature or bug-fix work
* the commit cannot be described without repeatedly using "and also"
* parts of the commit could be reverted independently
* parts of the commit have different purposes and no dependency on each other

The phrase "and also" is only a heuristic, not a hard rule. A coherent change can legitimately
contain several related modifications.

## Large commits

Commit size alone does not determine whether a commit is good or bad.

Prefer:

```text
one coherent logical change
```

over:

```text
many small commits with arbitrary boundaries
```

and prefer:

```text
several independent logical commits
```

over:

```text
one unrelated mega-commit
```

A large commit is acceptable when its changes are cohesive, reviewable, and intentionally part of
the same logical change.

## Terminology

The following terms describe different properties and should not be treated as interchangeable:

* **Atomic commit**: one commit represents one logical change.
* **Focused commit**: one commit stays focused on one task or objective.
* **Concern-based commit**: commits are separated by independent engineering concerns.
* **Conventional Commit**: a standardized commit-message format.
* **Commit type**: the semantic category of a commit, such as `feat`, `fix`, or `refactor`.
* **Scope**: the subsystem or area named in a Conventional Commit message.
* **Breaking change**: a change that can break compatibility for existing consumers.
* **Mega commit**: informal terminology for an unusually large or overly mixed commit. It is not a
  Git or Conventional Commits concept.
