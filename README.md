# Agent Skills

Reusable, progressively disclosed skills for coding and technical agents.

## Included

- `context7-expert`: current, version-aware library and platform documentation lookup.
- `copywriting-expert`: user-facing product and UI copy.
- `dizzy-commit`: repository-aware Git commit and push safety.
- `mermaid-diagrams-expert`: maintainable Mermaid diagrams for software documentation.
- `redis-expert`: Redis architecture, clients, search, clustering, observability, security, and semantic caching.

## Design principles

1. **Progressive disclosure**: `SKILL.md` is the routing and safety layer. Detailed procedures live in `references/`.
2. **Evidence before certainty**: version-sensitive or environment-specific claims must be verified rather than inferred.
3. **Project rules win**: repository and product-specific source-of-truth documents override portable defaults.
4. **Minimal mutation**: inspect freely, mutate only when the user explicitly authorizes the relevant side effect.
5. **Explicit uncertainty**: never invent tool availability, versions, renderer support, Git policy, or runtime behavior.
6. **Tool-aware workflows**: use available native tools first; degrade gracefully when a dependency is unavailable.
7. **No em dashes**: project preference applies to generated documentation, UI copy, and commit messages.

## Compatibility

Each skill is a normal directory containing `SKILL.md` and optional `references/`, so it can be copied or symlinked into an Agent Skills-compatible skills directory.
