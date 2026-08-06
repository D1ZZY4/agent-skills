# Validation, Rendering, and Export

Full detail for Step 3 in SKILL.md. The single biggest weakness in delivering hand-written
Mermaid syntax is that it's easy to produce something that looks plausible but fails to
render, or renders with a subtly wrong structure, and never notice.

## Validate before delivering, when possible

If a bash or shell tool is available, actually render the diagram rather than trusting the
syntax on sight:

```bash
npm install -g @mermaid-js/mermaid-cli   # once, if not already present
mmdc -i diagram.mmd -o diagram.svg
```

or without a global install:

```bash
npx @mermaid-js/mermaid-cli -i diagram.mmd -o diagram.svg
```

A clean exit with an output file means the syntax parsed. An error output means something in
the diagram is invalid, fix it before presenting the diagram as finished rather than handing
over syntax that was never actually checked.

If no rendering tool is available in the environment, say so plainly rather than silently
skipping validation, the same honesty principle as any other tool-unavailable situation:
present the diagram, but note it hasn't been rendered and to verify at
[mermaid.live](https://mermaid.live) before relying on it, especially for anything going into
a PR or shared doc.

## Common pitfalls

- **Unknown or misspelled keywords break the diagram.** `classDiagram` typo'd as
  `classDiagrm` doesn't degrade gracefully, it fails. Double check the diagram-type keyword
  against the relevant reference file.
- **Parameters fail silently, not loudly.** An unrecognized config option or theme variable is
  often just ignored rather than raising an error, so a diagram can render "successfully"
  while quietly not applying an intended style. If a theming option doesn't seem to be taking
  effect, check the option name against `advanced-features.md` rather than assuming it's a
  rendering issue.
- **Special characters need escaping or quoting.** Characters like `{`, `}`, `"`, and `:`
  inside labels can be misread as syntax rather than literal text. Wrap labels containing them
  in quotes: `A["Handles {retry} logic"]` rather than `A[Handles {retry} logic]`.
- **Line breaks inside labels use `<br/>`, not a literal newline**, a literal newline in the
  middle of a label definition usually breaks parsing rather than wrapping the text.
- **Reserved words as node IDs cause conflicts.** Avoid naming a flowchart node `end`, `class`,
  `state`, or other Mermaid keywords, even though it might look like a normal identifier.
- **Overcomplexity reads as a bug even when it isn't one.** A diagram that's technically valid
  but has too many crossing lines or too many entities is a design problem, not a syntax
  problem, see the splitting guidance in `diagram-type-selection.md`.
- **Missing relationships silently understate the model.** It's easy to add all the entities
  and forget a relationship between two of them, if reviewing a diagram against the actual
  code or schema it documents, check for connections that exist in reality but got left out.

## Export options

Only bring these up when the user actually needs an image file, not by default, most Mermaid
diagrams are consumed as rendered Markdown, not exported images.

- **[Mermaid Live Editor](https://mermaid.live)**: online editor with instant preview and
  PNG/SVG export, also the fastest way to manually sanity-check a diagram if no local
  rendering tool is available.
- **Mermaid CLI**: `npm install -g @mermaid-js/mermaid-cli`, then
  `mmdc -i input.mmd -o output.png` (or `.svg`, `.pdf`).
- **Docker**: `docker run --rm -v $(pwd):/data minlag/mermaid-cli -i /data/input.mmd -o
  /data/output.png`, useful when a local Node install isn't available or desired.

## Where diagrams render natively, no export needed

GitHub, GitLab, Notion, Obsidian, and Confluence all render fenced ` ```mermaid ` code blocks
directly in Markdown, no image export required for these. VS Code renders them with the
"Markdown Preview Mermaid Support" extension. Default to embedding as a Markdown code block
for anything going into a repo, wiki, or doc on one of these platforms, and only reach for
image export when the diagram needs to go somewhere that doesn't render Markdown (a
slide deck, a PDF report, an email).
