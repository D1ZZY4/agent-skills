# Skills Management via ctx7

Use only when the user explicitly asks to search, install, suggest, list, inspect, generate, or remove
AI coding skills through the `ctx7` CLI.

This reference is separate from ordinary documentation lookup because skills management may both access
remote content and write or delete local files.

## Command verification

CLI aliases and flags can change. If a command is not recognized, inspect the installed CLI's help rather
than guessing an alias or flag.

The current upstream CLI documents these command families:

```text
ctx7 skills install /owner/repo [name]
ctx7 skills search <keywords>
ctx7 skills suggest
ctx7 skills list
ctx7 skills remove <name>
ctx7 skills generate
ctx7 skills info /owner/repo
```

Use the installed CLI version's actual help output as the command reference when it conflicts with this
document.

## Read-only does not always mean non-networked

`skills list` may inspect local installations, while `skills search`, `skills suggest`, and `skills info`
may access remote registry or repository data. Treat any command that transmits data as subject to the
same query-confirmation rules in `security.md`.

In particular, `skills suggest` can inspect project dependency manifests. Do not run it as an innocent
background convenience when the resulting dependency names would be transmitted to a third party.

## Install

Repository identifiers use the `/owner/repo` form.

```bash
ctx7 skills install /owner/repository
ctx7 skills install /owner/repository skill-name
```

Before installation, confirm:

- source repository and skill name
- exact target agent
- project-local or user-global scope
- expected installation path
- whether authentication or network access is required

Target flags belong to the host adapter. Read `agent-adapters.md` rather than copying a flag from an
unrelated agent integration.

Do not use `--all` unless the user explicitly approves installing every skill from the repository.
Do not use `--global` unless the user explicitly chooses global scope.

## Search

Search terms are outbound data when the CLI queries the registry.

```bash
ctx7 skills search typescript testing
```

Propose and confirm the search terms before transmission when they contain project-specific information.

## Suggest

Suggestion may inspect files such as `package.json`, `requirements.txt`, `pyproject.toml`, `Cargo.toml`,
`go.mod`, or `Gemfile` and may use dependency information to query a registry.

```bash
ctx7 skills suggest
```

This command is not a harmless passive scan. Confirm the target scope and outbound-data implications
before running it.

## Generate

Generation is AI-powered and currently requires login according to the upstream CLI documentation.
Treat it as both network activity and a mutating operation because the resulting skill is written locally.

Before generating, confirm:

- requested expertise
- selected libraries, if any
- target scope
- expected output path
- authentication requirement

Do not silently log in to enable generation.

## List, info, and remove

```bash
ctx7 skills list
ctx7 skills info /owner/repository
ctx7 skills remove skill-name
```

Treat `remove` as destructive. Never remove a skill based only on an automated suggestion or stale
inventory.

After removal or installation, inspect the actual filesystem changes and report them.

## Post-operation checks

After a mutating command:

1. confirm the command's exit status
2. inspect created, modified, or removed files
3. verify the target scope
4. report any partial failure
5. do not assume rollback happened unless verified

Never claim that a skill was installed, generated, or removed merely because the command was attempted.
