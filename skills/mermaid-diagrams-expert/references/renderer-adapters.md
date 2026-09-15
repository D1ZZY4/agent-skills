# Renderer and Platform Adapters

Mermaid syntax is portable, but renderer behavior is not. Keep target-platform behavior in this
adapter reference rather than treating one editor, documentation host, or CLI as universal.

## Identify the target

Before selecting syntax or validating a diagram, identify:

1. where the diagram will render,
2. which Mermaid renderer that target uses,
3. the renderer version or supported feature set,
4. whether optional layouts or icon packs are available.

Use the project's declared dependencies or renderer configuration when available. If the target
version is unknown, choose a broadly supported syntax or provide a fallback.

## Capability boundaries

- A local Mermaid package, browser import, CLI, and hosted Markdown renderer may use different
  versions or configuration.
- A diagram that renders locally is not automatically supported by the publication target.
- `architecture-beta` needs Mermaid v11.1.0 or newer in a renderer that implements it.
- `packet` needs v11.0.0 or newer, `radar-beta` needs v11.6.0 or newer, `venn-beta` and
  `ishikawa-beta` need v11.12.3 or newer. Beta names include the suffix by design.
- Icon packs and ELK layout are optional capabilities. Detect them instead of assuming them.

## Platform notes

Use this table as a starting check, then verify against the target project. Hosts upgrade
at their own pace, so a local 12.x render does not prove GitHub or Notion support.

| Target | What to expect | Safe default |
|---|---|---|
| GitHub Markdown | Core flowcharts, sequence, class, state, ER, gantt, pie render well. Beta types, `architecture-beta`, C4 extensions, icon packs, and `xychart` often lag or are unavailable. | Flowchart, sequence, class, ER, state, git graph, gantt, pie. |
| GitLab Markdown | Similar to GitHub, with its own upgrade lag. Verify C4 and beta support per instance. | Same safe default as GitHub. |
| Notion, Obsidian, Confluence | Support fenced mermaid blocks, but version and config differ by app and plugin. | Core types only unless the workspace version is confirmed. |
| VS Code preview | Commonly needs the Markdown Preview Mermaid extension. Behavior follows the installed extension version. | Core types. Confirm extension version for beta use. |
| Local CLI (`mmdc`) | Follows the installed `@mermaid-js/mermaid-cli` version. Pin the version for reproducibility. | Any type the pinned version supports. Record the version. |
| mermaid.live | Tracks recent releases. Good for manual checks of new and beta types. | Use only for non-confidential diagrams, with approval. See `security.md`. |

Keep `@latest` in reference package-runner examples when the user explicitly approves a
temporary lookup or validation. Do not alter a project's dependency declaration merely to make
the example render.

## Confidentiality boundary

Do not send proprietary architecture, credentials, personal data, or private source code to an
online editor or hosted renderer. Prefer local validation for confidential material, or
anonymize labels and values before using a network service. Obtain approval before sending
diagram content outside the repository.