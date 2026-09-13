# Policy Configuration

This reference separates portable Git safety from repository-specific commit style. The skill
can work without a policy file, but it must inspect the repository before assuming conventions.

## Policy precedence

Resolve settings in this order:

1. Host or system safety constraints
2. Repository policy and contribution documentation
3. Explicit user preferences or instructions
4. Portable defaults in this skill

When two sources conflict, use the higher-precedence source and report the conflict if it
changes the requested operation.

## Portable defaults

Unless the repository or user says otherwise:

- Inspect ownership before mutating a dirty tree.
- Do not restore, delete, clean, or commit without explicit approval.
- Preserve the repository's configured Git author and upstream.
- Use Conventional Commit structure when the repository already uses it.
- Resolve commit grouping and message strategy per `references/commit-strategy.md`. Default
  is `auto`, overridable by repository policy or an explicit user instruction.
- Prefer a meaningful scope when one is clear, but do not invent a scope.
- Add a body for non-trivial changes or whenever the repository requires one.
- Use the repository's commit-language convention. If none exists, follow the user's language
  preference.
- Reject em dashes when the active punctuation policy disallows them. Technical strings,
  including commands, flags, and paths, must preserve their ASCII hyphens.
- When the repository signs commits, follow `references/commit-signing.md` for signing and
  verification. Changing signing, credentials, or identity is a separate mutation needing
  explicit approval.
- Treat prohibited words, fixed author identities, branch names, and remote names as policy
  inputs, never as universal defaults.

## What to inspect

Look for repository policy in the files and directories documented by the repository itself,
including contribution guidance, release documentation, project rules, and Git configuration.
Host-specific policy locations belong in the host adapter rather than in this portable core.

Do not assume any of these files exist. Do not cite an ignored or untracked file as the source
of a commit rule.

## Optional policy shape

A repository may document its preferences in any existing project policy file. A useful shape is:

```yaml
commit:
  convention: conventional
  scope: recommended
  body: required-for-nontrivial
  language: project-default
  prohibited_words: []
  punctuation:
    em_dash: disallow
  signing: required
  strategy: auto
  author:
    source: git-config
  upstream:
    source: git-config
```

The `strategy` field accepts the values from `references/commit-strategy.md`. The default is
`auto`; repository policy or an explicit user instruction can set any of the documented
values.

This is a documentation shape, not a requirement to add a new configuration file. Signing
follows `commit-signing.md` when the policy marks it required.

## Strict mode

Strict mode applies only the stricter rules found in repository policy or explicitly requested
by the user. It must not manufacture an author, email, branch, remote, language, or prohibited
word list. If a required strict setting is missing, ask before mutating configuration or making
the commit.
