# Policy Configuration

This reference separates repository-specific policy from portable Git safety.

The skill must work even when no dedicated policy file exists. Do not manufacture a policy file,
commit convention, author identity, remote name, branch name, or prohibited-word list.

## Priority order

Resolve applicable settings in this order:

1. Platform, system, and tool safety constraints.
2. Repository policy and contribution documentation.
3. Explicit user instructions and preferences.
4. Portable defaults in this skill.

A mandatory repository rule can override a portable style default. A user preference can override a
style default when the repository does not require the opposite. A user request does not authorize
a destructive operation that was not requested.

When a conflict changes the planned mutation, report the conflict before proceeding.

## What counts as repository policy

Inspect policy locations that the repository itself documents or conventionally uses, including:

- contribution and development guidance
- repository-maintained agent instructions
- release or workflow documentation
- project configuration that explicitly declares commit rules
- local Git configuration relevant to the operation

Do not assume any particular filename exists.

Host-specific requirements belong in `host-adapters.md`.

A repository policy file being present does not automatically make every line mandatory. Distinguish
normative rules from examples, recommendations, and explanatory prose.

## Portable defaults

Unless repository policy or the user says otherwise:

- inspect ownership before mutating a dirty tree
- preserve the configured author, committer, signing setup, remote, and upstream
- use Conventional Commits only when the repository already uses them or the user requests them
- prefer a meaningful scope when one is clear, but never invent one
- add a body for non-trivial changes when the policy permits or expects it
- follow the repository's documented commit language
- keep commit messages free of em dashes
- keep literal commands, paths, and flags exactly as valid ASCII syntax
- do not add emojis to commit messages
- resolve grouping through `commit-strategy.md`
- verify before and after mutation
- never cite an ignored or untracked file as a durable repository authority in a commit message

## Settings that may be policy-controlled

A repository policy may define:

```yaml
commit:
  convention: conventional
  scope: recommended
  body: required-for-nontrivial
  language: project-default
  prohibited_words: []
  punctuation:
    em_dash: disallow
    emoji: disallow
  signing: required
  strategy:
    grouping: auto
    message: conventional-commit
  author:
    source: git-config
  upstream:
    source: git-config
```

This is a documentation shape, not a requirement to create a new configuration file.

If the policy defines a stricter rule, apply that rule. If a field is absent, fall back to the next
priority level instead of guessing a value.

## Authorization is not policy

Policy answers "how the repository expects this operation to be performed".

Authorization answers "whether this operation is allowed right now".

A repository may require signed commits, but that does not itself authorize creating a commit.
A user may authorize a commit, but that does not authorize force-pushing it.

Keep those two questions separate.

## Identity and signing

Fixed author identities, signing keys, credentials, and `gpg.program` settings are policy inputs,
not defaults.

If the repository requires a specific identity or signer and the active configuration does not
satisfy it:

1. report the mismatch
2. do not silently change global configuration
3. obtain approval before changing configuration
4. verify the resulting identity before committing or pushing

See `strict-mode.md` and `commit-signing.md`.

## Upstream and remote policy

Do not infer that the remote is `origin` or that the branch is `main`.

Use the repository's configured relationship:

```bash
git remote -v
git branch --show-current
git rev-parse --abbrev-ref --symbolic-full-name '@{upstream}' 2>/dev/null || true
```

If policy requires a particular push destination and the current upstream does not match, stop before
changing tracking configuration or remotes.

## Ignored and untracked policy files

A locally present ignored or untracked file may still be useful for the current task, but do not cite
it in a durable commit message as though it were available to future repository readers.

Before citing a path as repository authority:

```bash
git check-ignore -v -- <file> || true
git ls-files --error-unmatch -- <file>
```

If it is not tracked, prefer stating the actual rule or rationale directly in the commit body.

If the file should be shared project policy, flag that its tracking state may be wrong rather than
silently changing it.

## Strict mode

Strict mode applies only when enabled by repository policy or explicitly requested by the user.

It must not manufacture missing values. If a strict setting is required but missing, stop before
the relevant mutation and ask for the missing information or authorization to change configuration.
