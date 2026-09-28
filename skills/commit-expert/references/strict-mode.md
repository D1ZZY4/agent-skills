# Strict Mode Rules

Strict mode adds stronger validation on top of the default workflow. It is active only when enabled
by repository policy or explicitly requested by the user.

Strict mode is fail-closed for required metadata and verification. It never invents missing values.

## Author policy

Use the repository's configured Git author by default.

Inspect the effective identity when strict mode requires author verification:

```bash
git var GIT_AUTHOR_IDENT
git var GIT_COMMITTER_IDENT
```

When a repository policy requires a specific author, verify that policy before changing any identity
configuration.

Never invent:

- a name
- an email
- a provider identity
- a signing key

If the configured identity does not satisfy a mandatory policy and the commit is not yet public:

1. stop
2. report the mismatch
3. ask for authorization before changing identity configuration or rewriting the commit

After a commit, verify:

```bash
git log -1 --format="%an <%ae>"
```

When committer identity also matters:

```bash
git log -1 --format="%cn <%ce>"
```

## Strict message validation

When strict mode requires Conventional Commits:

- validate `type`
- validate `scope` only when required
- validate imperative summary style
- validate prohibited words from resolved policy
- reject em dash characters
- reject emojis
- validate body/footer requirements
- validate breaking-change metadata when applicable
- validate trailer syntax against the repository's policy

Do not reject a scope merely because it is absent unless policy requires a scope.

Do not invent a scope to satisfy a generic template.

## Strict staging validation

Before commit:

```bash
git diff --cached --name-status
git diff --cached --stat
git diff --cached --check
```

The staged file set must match the approved scope.

An unexpected path is a stop condition, not a minor warning.

## Strict verification

Run every relevant repository-required check that is available and authorized.

For each check report:

- command
- pass/fail/skipped/not-applicable
- material error when failed or skipped

If a mandatory check cannot run, do not represent the commit as fully verified.

## Strict signing

When policy requires signed commits:

1. inspect effective signing configuration
2. create the commit using the configured signer
3. verify the signature before push
4. verify every commit in the push range when more than one commit is being published

Follow `commit-signing.md`.

Never switch keys or keyrings to make verification appear successful.

## Strict history safety

Do not amend, rebase, squash, force-push, delete remote branches, or rewrite history unless that
specific operation has been explicitly authorized.

Never rewrite a commit that has already been pushed merely to satisfy strict message or author rules.

## Strict branch/upstream safety

Before a push:

```bash
git status --short --branch
git branch --show-current
git rev-parse --abbrev-ref --symbolic-full-name '@{upstream}' 2>/dev/null || true
git remote -v
```

A missing or unexpected upstream is a stop condition when strict policy requires a specific destination.

Do not create tracking configuration merely to make the command work.

## Strict failure behavior

On any failed required check, hook, signature, author validation, staged-scope validation, or push:

- stop the mutation sequence
- preserve the repository state
- report the exact failure
- do not bypass the failing control automatically
- do not use destructive recovery commands

## Strict mode does not mean "clean harder"

A dirty working tree containing user-owned changes is valid.

Strict mode requires correct ownership reporting and scope control. It does not permit deleting,
restoring, cleaning, or resetting unrelated work.
