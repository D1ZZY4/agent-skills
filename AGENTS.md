# AGENTS.md

## Project overview

This repository contains reusable custom agent skills for documentation lookup,
product copywriting, README creation, diagrams, disciplined Git commits, and Redis operations.

Each skill is a standard directory containing `SKILL.md` and optional `references/`.
`SKILL.md` is the routing and safety layer; detailed procedures live in `references/`.

## User preferences

- Do not use em dashes in generated documentation, UI copy, or commit messages.
- Keep literal commands, flags, paths, and identifiers on their exact ASCII hyphens.

## Repository structure

- `skills/context7-expert/` - version-aware library and platform documentation lookup
- `skills/copywriting-expert/` - user-facing product and UI copy guidance
- `skills/commit-expert/` - repository-aware Git commit and push safety
- `skills/mermaid-diagrams-expert/` - maintainable Mermaid diagrams for software documentation
- `skills/redis-expert/` - Redis architecture, clients, search, clustering, observability, security, and semantic caching
- `skills/create-readme-expert/` - README creation guidance for software projects
- `CHANGELOG.md` - project changelog with per-skill version tracking
- `README.md` - project overview and usage
- `CONTRIBUTING.md` - contributor guide for humans
- `skills.sh.json` - skills.sh directory grouping
- `plugin.json`, `gemini-extension.json`, `.claude-plugin/` - official agent marketplace manifests
- `assets/logos/` - verified agent logos used by the README
- `LICENSE` - SSPL-1.0 License, Copyright (c) 2026 D1ZZY4

## Design principles

1. **Progressive disclosure**: route through `SKILL.md`; load procedures from `references/` only as needed.
2. **Evidence before certainty**: version-sensitive or environment-specific claims must be verified rather than inferred.
3. **Project rules win**: repository and product-specific source-of-truth documents override portable defaults.
4. **Minimal mutation**: inspect freely, mutate only when the user explicitly authorizes the relevant side effect.
5. **Explicit uncertainty**: never invent tool availability, versions, renderer support, Git policy, or runtime behavior.
6. **Tool-aware workflows**: use available native tools first; degrade gracefully when a dependency is unavailable.
7. **No em dashes**: project preference applies to generated documentation, UI copy, and commit messages.

## Versioning

This repository uses two version tracks:

- Project version: the version of the repository as a whole, recorded in `CHANGELOG.md` release
  headings. Format: `1.Y.Z`. The first number marks major repository-level changes, the second
  notable releases (up to `20`), the third patches.
- Skill version: each skill tracks its own version in `SKILL.md` `metadata.version`. Format: `1.Y.Z`.
  Major starts at `1`. Minor grows with skill maturity and review feedback. A skill version may
  lag behind or lead the project version; they are independent.

Keep the first number at `1` unless the change justifies a new major track.
Do not start a version with `0`.

## Workflow rules

- Sign every commit and tag with the repository GPG key; never push an unsigned commit.
- Do not push without explicit user authorization.
- Do not commit while the user is reviewing changes without explicit authorization for the commit.
- In `CHANGELOG.md`, always keep `[Unreleased]` as the first version section, above any released versions.
- Update `CHANGELOG.md` before committing whenever the change set is worth recording.
