# Security

Mermaid renders text into SVG and HTML. Treat diagram source as untrusted input when it comes from outside the repository.

## What to protect

- Secrets, tokens, passwords, private keys, and connection strings. Never place them in nodes, labels, or examples, even as placeholders that look real.
- Personal data and customer data. Anonymize names, emails, and account IDs before diagramming.
- Private architecture and source paths. Prefer local validation for confidential diagrams. Obtain approval before pasting them into an online editor or renderer.

## Injection risks

Mermaid has shipped XSS and CSS injection fixes in the past, including issues around `classDef`, theme config, and state diagram handling on the 9.x and 10.x lines. Assume the risk remains on any renderer you did not pin:

- Do not render diagram source from untrusted users without the sanitizer and sandbox the host provides.
- For public sites, render in a sandboxed iframe when the platform supports it. This blocks script execution from diagram content.
- Keep the Mermaid package pinned to a version with current security fixes. Do not downgrade to make an old diagram render.
- Review `click` handlers, embedded URLs, `classDef`, and frontmatter `config` before merging. These are the fields most likely to carry a payload.

## Safe practice in this repo

- Use `example.com`, `192.0.2.0/24`, and clearly fake tokens in examples.
- Keep real hosts, bucket names, and internal URLs out of committed diagrams.
- Report the renderer and Mermaid version when a diagram behaves unexpectedly instead of disabling sanitization to make it render.

## Sources

- https://mermaid.js.org/intro/ (Security and safe diagrams section)
- https://github.com/mermaid-js/mermaid (Security policy and release notes)
