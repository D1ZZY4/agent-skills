# AGENTS.md

Project-level rules and guidance for agent behavior in this repository.

## Project overview

This repository contains reusable custom agent skills for documentation lookup,
UI copywriting, disciplined Git commits, and Mermaid diagrams.

Each skill is a normal directory containing `SKILL.md` and optional `references/`.
`SKILL.md` is the routing and safety layer; detailed procedures live in `references/`.

## User preferences

- Do not use em dashes in generated documentation, UI copy, or commit messages.
- En dashes are acceptable when used correctly as punctuation.
- Do not treat an en dash as a replacement for ASCII hyphens in commands,
  flags, paths, or identifiers.

## Repository structure

- `context7-expert/` - version-aware library and platform documentation lookup
- `copywriting-expert/` - user-facing product and UI copy guidance
- `dizzy-commit/` - repository-aware Git commit and push safety
- `mermaid-diagrams-expert/` - maintainable Mermaid diagrams for software documentation
- `redis-expert/` - Redis architecture, clients, search, clustering, observability, security, and semantic caching
- `create-readme-expert/` - README creation guidance for software projects
- `CHANGELOG.md` - project changelog with per-skill version tracking
- `README.md` - project overview and design principles
- `LICENSE` - MIT License, Copyright (c) 2026 D1ZYY4

## Design principles

1. **Progressive disclosure**: `SKILL.md` is the routing and safety layer. Detailed procedures live in `references/`.
2. **Evidence before certainty**: version-sensitive or environment-specific claims must be verified rather than inferred.
3. **Project rules win**: repository and product-specific source-of-truth documents override portable defaults.
4. **Minimal mutation**: inspect freely, mutate only when the user explicitly authorizes the relevant side effect.
5. **Explicit uncertainty**: never invent tool availability, versions, renderer support, Git policy, or runtime behavior.
6. **Tool-aware workflows**: use available native tools first; degrade gracefully when a dependency is unavailable.
7. **No em dashes**: project preference applies to generated documentation, UI copy, and commit messages.

## Versioning

Each skill has its own semantic version in `SKILL.md` frontmatter and `metadata.version`.
Major version starts at 1. Minor increases by skill maturity.
See `CHANGELOG.md` for per-skill version history.

## Workflow rules

- Do not push without explicit user authorization.
- Do not commit without explicit user authorization when the user is reviewing changes.
- In `CHANGELOG.md`, always keep `[Unreleased]` as the first version section, above any released versions.
- Update `CHANGELOG.md` before committing whenever the change set is notable enough to record.
