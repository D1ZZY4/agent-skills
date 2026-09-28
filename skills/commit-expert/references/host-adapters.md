# Host and Upstream Adapters

The core skill is Git-provider neutral. Provider-specific behavior belongs here so the core workflow
does not accidentally assume GitHub, GitLab, Bitbucket, or a particular self-hosted service.

## Generic repository adapter

Start with ordinary Git state:

```bash
git remote -v
git branch --show-current
git rev-parse --abbrev-ref --symbolic-full-name '@{upstream}' 2>/dev/null || true
```

Do not assume:

- remote name `origin`
- branch name `main`
- a configured upstream
- a specific hosting provider
- a provider CLI is installed

## Determine the host from configured data

Use the repository's configured remote to identify the provider when needed.

Do not print credentials embedded in remote URLs.

Provider detection is descriptive only. It does not change the permission model.

## Hosting-specific rules

GitHub, GitLab, Bitbucket, and self-hosted Git servers can differ in:

- protected branch settings
- required reviews
- required status checks
- server-side hooks
- signed-commit display
- push permissions
- merge and pull request workflows
- branch naming and protection conventions

Treat these as adapter behavior.

Read repository contribution and hosting guidance before pushing or creating a pull request.

## Provider CLIs

Do not assume `gh`, `glab`, `bb`, or another provider CLI exists.

If a provider CLI is available and repository policy explicitly uses it, use it only within the
authorized operation. A provider CLI does not bypass the Git skill's authorization boundaries.

## Trailers and hosting display

Commit-message trailers are part of Git's message model. A hosting service may display or interpret
some trailers specially.

Only add a co-author identity when the repository/user permits it and the provider actually supplied
the identity.

Use standard form:

```text
Co-authored-by: Name <email>
```

Never invent an email or infer one from a username.

## Identity changes

Changing any of the following is a separate mutation:

- `user.name`
- `user.email`
- signing configuration
- signing keys
- credentials
- remotes
- push/fetch refspecs
- branch tracking configuration

Explain the intended target and obtain explicit authorization before changing them.
