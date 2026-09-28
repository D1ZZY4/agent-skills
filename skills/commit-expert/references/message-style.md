# Message Style Rules

This reference defines commit message structure, subject and body rules, trailer behavior, and the
commit type vocabulary used when Conventional Commits applies.

These are style rules unless repository policy makes them mandatory.

## Format

```text
<type>(<scope>): <short imperative summary>

<body when required>

<footer/trailers when required>
```

For a breaking change using Conventional Commits:

```text
feat(api)!: change response contract

Explain the compatibility impact.

BREAKING CHANGE: clients must use the new response field.
```

## Subject line

- Use `type(scope): summary` when Conventional Commits is required or explicitly requested.
- Include a scope when repository policy requires it or when a meaningful scope is clear.
- Never invent a scope merely to satisfy a template.
- Use imperative wording such as `add`, `fix`, `remove`, or `rename`.
- Target roughly 50 characters; treat 72 as a practical upper boundary unless the repository has
  another convention.
- Do not add a trailing period.
- Do not use em dash characters (U+2014).
- Do not use emojis.
- Preserve literal ASCII hyphens in commands, flags, paths, and technical identifiers.
- Follow the repository's documented language convention or the user's explicit language preference.

## Body

Add a body when:

- repository policy requires one
- the change is non-trivial
- the compatibility impact needs explanation
- a security fix needs context
- a migration needs operator guidance
- the diff does not make the reason obvious

Explain what changed and why it matters. Avoid narrating the agent's process.

For multiple distinct points, use Markdown bullets:

```text
fix(auth): reject expired refresh tokens

- Reject expired tokens before session lookup
- Keep the existing error contract for valid failures

Prevents stale refresh sessions from reaching downstream
authorization checks.
```

Keep the body readable and reasonably wrapped. Repository conventions take precedence over an
arbitrary line width.

## Footer and trailers

Keep structured references after the body, separated by a blank line.

Common examples include:

```text
Closes #42
Refs #17
BREAKING CHANGE: existing clients must migrate
Co-authored-by: Name <email>
```

Use only trailers supported by repository policy or the user's explicit request.

Do not invent issue numbers, emails, identities, or provider metadata.

## AI co-author trailer

If an agentic coding provider supplies an official co-author identity and the repository/user allows
co-authorship, use:

```text
Co-authored-by: Specific Agent Name <provider-issued-address>
```

Rules:

- use the exact provider-issued email
- use the specific known model/tool identity when the provider supplies it
- do not fabricate a model version
- do not infer an email from a username
- put the trailer at the bottom of the message
- keep AI involvement out of the subject and body

Git treats trailer lines as structured message metadata; hosting services may apply their own display
or attribution rules.

## Never include

Unless repository policy explicitly allows otherwise, do not include:

- agent process narration
- generic text such as "Update documentation" when the diff supports a precise description
- fabricated issue references
- fabricated authorship
- emojis
- em dash characters
- unexplained policy citations to ignored or untracked local files

## Derive from the diff

Construct the message from:

1. the resolved repository policy
2. the actual staged diff
3. the compatibility/security/migration impact
4. the user's explicit wording preference

Do not derive the message from a checklist, task title, or plan alone.

## Commit type reference

| Type | Use |
| --- | --- |
| `feat` | New feature or user-visible behavior |
| `fix` | Bug fix |
| `docs` | Documentation-only change |
| `refactor` | Restructure without intended behavior change |
| `perf` | Performance improvement |
| `test` | Add or fix tests |
| `style` | Formatting or whitespace only, with no logic change |
| `build` | Build system or dependency/build tooling change |
| `ci` | CI configuration |
| `chore` | Other maintenance that does not fit the above |
| `revert` | Revert a prior change |

Do not force a type when the repository uses a different vocabulary.

## Breaking changes

When the repository uses Conventional Commits, a breaking change is commonly marked with `!` and
explained with a `BREAKING CHANGE:` footer or repository-equivalent notation.

The actual compatibility impact matters more than the symbol. Do not label a change breaking merely
because it is large.

## Sources checked

- Conventional Commits specification:
  https://www.conventionalcommits.org/en/v1.0.0/#specification
- Git commit documentation:
  https://git-scm.com/docs/git-commit
- Git trailer documentation:
  https://git-scm.com/docs/git-interpret-trailers
