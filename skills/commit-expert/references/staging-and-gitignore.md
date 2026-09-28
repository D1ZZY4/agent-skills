# Staging Discipline and Gitignore Safety

The index is the exact boundary of the next commit. Treat staging as a deliberate selection step,
not as cleanup.

## Ownership before staging

Before staging, determine which changes belong to the current task.

```bash
git status --short --branch
git diff --name-status
git diff --cached --name-status
```

Classify candidates as:

- task-owned changes
- pre-existing user changes
- generated or derived files
- ignored files
- files with unclear ownership

Unclear ownership is not permission to stage. Leave it untouched and report the ambiguity.

## Atomic commits

One commit should represent one logical change.

Valid logical units can span multiple files or directories when they are one coherent change:

- implementation and its tests
- a feature and required documentation
- a schema change and the migration that makes it usable
- a dependency update together with required lockfile changes

Do not split a coherent change merely because it crosses directories.

Split independent concerns when they can be reviewed, reverted, or understood independently.

## Check ignore rules before staging

Before staging a new or unknown file:

```bash
git check-ignore -v -- <file>
```

For tracked status:

```bash
git ls-files --error-unmatch -- <file>
```

Interpret the result carefully:

- tracked files remain tracked even if a later `.gitignore` rule matches them
- new files matched by `.gitignore` are presumed intentionally excluded
- an ignored new file is not staged with normal `git add`
- do not use `git add -f` unless the user explicitly names and authorizes the ignored file
- if the ignore status contradicts project intent, flag the gap instead of guessing

## Never cite an ignored or untracked file as commit authority

A commit message must remain understandable to someone who clones the repository later.

Do not write a body such as:

```text
Per local-prompt.md, keep the generated files out of the commit.
```

when `local-prompt.md` is ignored or untracked.

Instead write the actual rule:

```text
Keep generated artifacts out of version control because the repository
rebuilds them during the release workflow.
```

The same principle applies to temporary instructions, local prompts, logs, and machine-specific notes.

## Staging commands

Prefer explicit pathspecs:

```bash
git add -- path/to/file-a path/to/file-b
```

For a deletion that is already part of the intended task, stage the exact path after review.

Avoid:

```bash
git add .
git add -A
```

unless the entire repository diff has already been inspected and the whole diff is intentionally
one coherent change.

## Verify the index before commit

Always inspect the staged result after staging:

```bash
git diff --cached --name-status
git diff --cached --stat
git diff --cached --check
```

When the change is security-sensitive or otherwise high-risk, inspect the full staged patch:

```bash
git diff --cached
```

The working-tree diff and staged diff can differ. Verify the staged diff, not just the working tree.

## Gitignore changes are special

If `.gitignore` is itself being changed:

1. inspect both the old and new ignore behavior
2. verify which newly visible files are affected
3. do not stage newly untracked files just because the ignore rule changed
4. keep the `.gitignore` change and any affected files grouped only when they form one logical change

Do not use a broad add command to discover the consequences of an ignore-rule change.

## Generated and derived files

Generated files require repository-specific evidence.

Do not add them merely because they appeared after a build or test run. Check repository guidance,
existing history, and ignore rules first.

Conversely, do not delete or unstage generated files simply because they look derived. Their status may
be intentional.

## Submodules and nested repositories

A parent repository may report a submodule as modified without exposing the nested repository's full
diff through the parent index.

Do not enter or mutate a nested repository merely because the parent shows a change.

Treat nested repository mutations as a separate scope unless the user explicitly asks for them.
