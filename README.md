# Agent Skills

[![skills.sh](https://skills.sh/b/D1ZZY4/agent-skills)](https://skills.sh/D1ZZY4/agent-skills)

Reusable, progressively disclosed skills for coding and technical agents. Each skill is a normal directory containing `SKILL.md` and optional `references/`, so it can be copied or symlinked into any Agent Skills-compatible skills directory.

## Install

```bash
npx skills add D1ZZY4/agent-skills
```

This installs all skills in this repository and makes them available to your AI agent.

## Skills

### Documentation and content

- `context7-expert`: current, version-aware library and platform documentation lookup; auto-loads but always proposes the query to the user before running it.
- `copywriting-expert`: user-facing product and UI copy, including accessibility text.
- `create-readme-expert`: source-driven README creation, improvement, and audit.
- `mermaid-diagrams-expert`: maintainable Mermaid diagrams for software documentation.

### Development workflow

- `dizzy-commit`: repository-aware Git commit and push safety.
- `redis-expert`: Redis architecture, clients, search, clustering, observability, security, and semantic caching.

## Setup

Copy a skill directory to the skills path supported by your agent. The standard convention is a `SKILL.md` routing file plus optional `references/` for detailed procedures. See [AGENTS.md](AGENTS.md) for the rules these skills follow.

## Compatible agents

These skills are compatible with tools that support the Agent Skills format, including:

- Claude Code
- Cursor
- GitHub Copilot
- Gemini CLI
- Hermes
- OpenCode
- Cline

Each agent stores skills in its own configuration directory. Check your agent's documentation for the correct installation path.

## Design principles

1. **Progressive disclosure**: `SKILL.md` is the routing and safety layer. Detailed procedures live in `references/`.
2. **Evidence before certainty**: version-sensitive or environment-specific claims must be verified rather than inferred.
3. **Project rules win**: repository and product-specific source-of-truth documents override portable defaults.
4. **Minimal mutation**: inspect freely, mutate only when the user explicitly authorizes the relevant side effect.
5. **Explicit uncertainty**: never invent tool availability, versions, renderer support, Git policy, or runtime behavior.
6. **Tool-aware workflows**: use available native tools first; degrade gracefully when a dependency is unavailable.
7. **No em dashes**: project preference applies to generated documentation, UI copy, and commit messages.

## Versioning

Two independent version tracks are recorded in [CHANGELOG.md](CHANGELOG.md):

- **Project version** (`1.Y.Z`): the repository as a whole.
- **Skill version** (`1.Y.Z`): each skill tracks `metadata.version` in its own `SKILL.md`.

## License

SSPL-1.0. Copyright (c) 2026 D1ZZY4. See [LICENSE](LICENSE).