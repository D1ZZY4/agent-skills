# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

[Detailed Changelog](#per-skill-changelog)
---

## [Unreleased]

### Added

- AGENTS.md as the canonical project rules file.
- Symlinks so CLAUDE.md and replit.md both point to AGENTS.md.
- create-readme-expert skill with proactive trigger, bundled references, and README-structure guidance.
- `examples/` folder with README-1.md, URL.md, and EXAMPLES.md.
- `Examples` section in create-readme-expert SKILL.md listing bundled examples.
- Step 2 now loads `examples/README-1.md` when choosing README structure.

### Changed

- Removed scripts/ folder and cleaned up AGENTS.md accordingly.
- Renamed `references/examples-and-anti-patterns.md` to `references/anti-patterns.md`.

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
