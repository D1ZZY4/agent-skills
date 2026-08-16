# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

[Detailed Changelog](#per-skill-changelog)
---

## [Unreleased]

### context7-expert

- Bumped metadata.version to 1.9.0.
- Added priority hierarchy to SKILL.md for conflict resolution.
- Strengthened risk classification in risk-and-budget.md with concrete high-risk examples.
- Added minimum-fetch rule to risk-and-budget.md.
- Added environment detection guidance to cli-mode.md for PowerShell, cmd.exe, and container/CI environments.
- Added explicit "do not use Context7" boundaries to SKILL.md Step 0.
- Strengthened setup.md to defer to the target agent's own documentation.
- Added package-scope disambiguation guidance to selection-and-query-writing.md.
- Clarified that Context7 confirms documentation, not user code correctness, in verification-and-failure.md.

### create-readme-expert

- Bumped metadata.version from 1.7.0 to 1.9.0.
- Fixed SKILL.md Examples section to list actual bundled example files.
- Replaced hardcoded MIT placeholder in README-1.md with generic license reference.
- Fixed typo in readme-structures.md: Prerequisiteses -> Prerequisites.

### redis-expert

- Resolved DIALECT 3 contradiction between dialect.md and search query examples.
- Removed eval-harness language and vague gold-dataset claims from command-selection.md.
- Aligned network.md command-renaming guidance with SKILL.md preference order.
- Removed hardcoded 0.9 similarity threshold default from best-practices.md.
- Redirected LangCache pointer in python-redisvl.md to this skill's semantic-cache references.
- Annotated undefined embedding/LLM placeholders in vector-query.md, hybrid-search.md, rag-pattern.md, and langcache-usage.md.
- Annotated missing collections import in command-selection.md bad example.

### copywriting-expert

- Removed self-referential phrasing from SKILL.md routing layer.

### mermaid-diagrams-expert

- Removed self-referential phrasing from SKILL.md routing layer.

[⬆ Back to top](#changelog)

---

## [1.7.0] - 2026-08-16

### Added

- Step 2 in create-readme-expert now loads `references/readme-structures.md` only; `examples/README-1.md` is conditional for new README creation.
- `references/external-readme-sources.md` now includes structural-inspiration-only warning with do-not-copy rules.
- `references/anti-patterns.md` now includes a correction line for unsupported claims.
- `examples/README-missing-information.md` wording tightened from "inferred" to "documented only from".
- `examples/EXAMPLES.md` now separates reference material from the examples list.

### Changed

- Bumped create-readme-expert metadata.version to 1.7.0.
- Added workflow rules to AGENTS.md: push/commit authorization, `[Unreleased]` position rule, and changelog update guidance.

[⬆ Back to top](#changelog)

---

## [1.6.0] - 2026-08-16

### Added

- Change scope control in SKILL.md to match README change size to user request.
- Missing information handling mechanism in SKILL.md.
- Audience identification section in readme-structures.md.
- Repository inspection checklist in verification-and-failure.md.
- Preserve existing README voice rules in voice-and-tone.md.
- `examples/README-unsupported-claims.md` failure case example.
- Release/update behavior in proactive-trigger.md.
- Dependency documentation rule in readme-structures.md.

### Changed

- Bumped create-readme-expert metadata.version to 1.5.0.
- Narrowed proactive trigger to user-facing workflow, installation, public API, or CLI changes.
- Added placeholder warning to `examples/README-1.md`.

### context7-expert

- Bumped context7-expert metadata.version to 1.6.0.
- Added risk-tiered operation budget in risk-and-budget.md.
- Added traceability requirements in mcp-mode.md and cli-mode.md.
- Tightened safety boundaries in setup.md for install/setup/auth/skills-generate.
- Added agent-adapters.md for host adapter generalization.
- Rewrote verification-and-failure.md with concrete rules and hard safety boundaries.

[⬆ Back to top](#changelog)

---

## [1.5.0] - 2026-08-16

### Added

- `references/external-readme-sources.md`: moved from `examples/URL.md` as source material.

### Changed

- Bumped create-readme-expert version from 1.2.0 to 1.3.0.
- Upgraded `examples/README-library-adaptive.md`, `README-cli-adaptive.md`, and `README-missing-information.md` to evidence-based format.
- Step 4 now loads examples conditionally by project type.
- Step 0/1 repetition cleaned up in SKILL.md.
- Narrowed proactive trigger to user-facing workflow, installation, public API, or CLI changes.
- Added placeholder warning to `examples/README-1.md`.

[⬆ Back to top](#changelog)

---

## [1.4.0] - 2026-08-16

### Added

- `examples/README-library-adaptive.md`: library example showing source-driven documentation.
- `examples/README-cli-adaptive.md`: CLI example showing command verification.
- `examples/README-missing-information.md`: incomplete project example showing uncertainty handling.
- Step 4 now loads all bundled README examples for structural and tonal inspiration.

### Changed

- Bumped create-readme-expert version from 1.1.0 to 1.2.0.

[⬆ Back to top](#changelog)

---

## [1.3.0] - 2026-08-16

### Added

- Per-skill changelog sections with individual version tracking.
- Author and license metadata to every skill frontmatter.
- Proactive trigger references across skills.
- verification-and-failure reference across skills.
- Self-contained references across all skills.
- CHANGELOG.md with back-to-top navigation and per-skill version tables.
- MIT LICENSE with author D1ZYY4.
- README.md with design principles, validation instructions, and skill list.
- AGENTS.md as the canonical project rules file.

### Changed

- Improved changelog navigation with back-to-top links.
- Skill versions now reflect actual commit age rather than being uniform.
- Major version starts at 1 across all skills; minor increases by skill maturity.

### Changed

- Consolidated project rules into AGENTS.md.
- Created symlinks so CLAUDE.md and replit.md both point to AGENTS.md.

### Fixed

- Removed unnecessary validation section from README.
- Removed duplicate top back-to-top link from CHANGELOG.
- Restored missing Per-skill changelog heading.
- Removed duplicate 1.3.0 entries from mermaid-diagrams-expert and redis-expert tables.

[⬆ Back to top](#changelog)

---

## [1.2.0] - 2026-08-11

### Added

- Explicit skill versions in frontmatter.
- Evidence hierarchy and version-awareness to Context7 workflows.
- Renderer/version compatibility checks for Mermaid.
- Dependency-free repository validator.
- Shared verification and failure-handling guidance.
- Repository README and VERSION metadata.
- Proactive trigger references for context7-expert, dizzy-commit, and mermaid-diagrams-expert.

### Changed

- Tightened trigger conditions to reduce unnecessary tool usage.
- Strengthened copywriting guidance around accessibility, localization, and unsupported claims.
- Tightened Git mutation boundaries and verification language.

### Fixed

- Removed leftover TODO from copywriting anti-pattern reference.
- Added validation coverage for broken local references, duplicate names, malformed frontmatter, and forbidden em dashes.

[⬆ Back to top](#changelog)

---

## [1.1.0] - 2026-07-13

### Added

- Initial release of agent-skills repository.
- context7-expert: current, version-aware library and platform documentation lookup.
- copywriting-expert: user-facing product and UI copy guidance.
- dizzy-commit: repository-aware Git commit and push safety.
- mermaid-diagrams-expert: maintainable Mermaid diagrams for software documentation.
- redis-expert: Redis architecture, clients, search, clustering, observability, security, and semantic caching.
- Progressive disclosure pattern: SKILL.md routing layer with references/ for detailed content.
- Validation script for frontmatter, required files, broken references, duplicate names, and forbidden em dashes.

[⬆ Back to top](#changelog)

---

## Per-skill changelog

### Version comparison

| Version | Date | Skills | Key changes |
|---------|------|--------|-------------|
| 1.6.0 | 2026-08-16 | 1 | create-readme-expert review feedback: scope control, missing info handling, audience id, inspection checklist, voice preservation, unsupported claims example |
| 1.5.0 | 2026-08-16 | 1 | create-readme-expert review fixes, evidence-based examples, version bump to 1.3.0 |
| 1.4.0 | 2026-08-16 | 1 | create-readme-expert examples additions, version bump to 1.2.0 |
| 1.3.0 | 2026-08-16 | 5 | Self-contained references, proactive triggers, verification-and-failure references, license/metadata across skills |
| 1.2.0 | 2026-08-11 | 5 | Skill versions, evidence hierarchy, proactive triggers, verification guidance |
| 1.1.0 | 2026-07-13 | 5 | Initial release, progressive disclosure pattern, validation |

### context7-expert

| Version | Date | Changes |
|---------|------|---------|
| 1.5.0 | 2026-08-16 | Evidence hierarchy, version-awareness, MCP/CLI mode selection, proactive trigger |
| 1.3.0 | 2026-08-16 | License, metadata, self-contained references, verification-and-failure reference |
| 1.2.0 | 2026-08-11 | Evidence hierarchy, version-awareness, MCP/CLI mode selection, proactive trigger |
| 1.1.0 | 2026-07-13 | Initial release |

[⬆ Back to top](#changelog)

### copywriting-expert

| Version | Date | Changes |
|---------|------|---------|
| 1.3.0 | 2026-08-16 | Accessibility/localization strengthening, proactive trigger, self-contained references, verification-and-failure reference |
| 1.2.0 | 2026-08-11 | Accessibility/localization strengthening, proactive trigger, self-contained references |
| 1.1.0 | 2026-07-13 | Initial release |

[⬆ Back to top](#changelog)

### dizzy-commit

| Version | Date | Changes |
|---------|------|---------|
| 1.10.0 | 2026-08-16 | Highest maturity tier, tightened mutation boundaries, verification language, proactive check-in flow |
| 1.3.0 | 2026-08-16 | License, metadata, self-contained references, verification-and-failure reference |
| 1.2.0 | 2026-08-11 | Evidence hierarchy, version-awareness |
| 1.1.0 | 2026-07-13 | Initial release |

[⬆ Back to top](#changelog)

### mermaid-diagrams-expert

| Version | Date | Changes |
|---------|------|---------|
| 1.2.0 | 2026-08-11 | Renderer/version compatibility, proactive trigger, misc diagram types |
| 1.1.0 | 2026-07-13 | Initial release |

[⬆ Back to top](#changelog)

### redis-expert

| Version | Date | Changes |
|---------|------|---------|
| 1.1.0 | 2026-07-13 | Initial release |

[⬆ Back to top](#changelog)

### create-readme-expert

| Version | Date | Changes |
|---------|------|---------|
| 1.6.0 | 2026-08-16 | Change scope control, missing info handling, audience id, repository inspection checklist, preserve README voice, unsupported claims example, release trigger, dependency rule |
| 1.4.0 | 2026-08-16 | External README sources moved to references, Step 4 conditional loading, placeholder warning |
| 1.3.0 | 2026-08-16 | Evidence-based examples, conditional Step 4 loading, proactive trigger narrowing, placeholder warning |
| 1.2.0 | 2026-08-16 | Added adaptive README examples, Step 4 loads all bundled examples |
| 1.1.0 | 2026-07-13 | Initial release |

[⬆ Back to top](#changelog)
