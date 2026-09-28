---
name: mermaid-diagrams-expert
description: >
  Create maintainable Mermaid diagrams for software documentation, including flowcharts,
  sequence, class, ER, C4, architecture, state, git, gantt, chart, kanban, packet, venn,
  and ishikawa diagrams. Trigger when structure, relationships, sequencing, or architecture
  would be clearer visually, especially for persistent README, wiki, PR, or design-document
  diagrams. Verify the target renderer and Mermaid version before using version-sensitive
  or beta syntax.
license: SSPL-1.0
metadata:
  version: 1.6.0
  author: D1ZZY4
  priority: medium
---

# Mermaid Diagrams Expert

## Purpose

Create maintainable Mermaid diagrams for software documentation when structure,
relationships, sequencing, or architecture would be clearer visually: flowcharts, sequence,
class, ER, C4, architecture, state, git, gantt, chart, kanban, packet, venn, and ishikawa
diagrams. Verify the target renderer and Mermaid version before using version-sensitive or
beta syntax. Load the references needed for the chosen diagram type.

## Core principles

1. Use a diagram only when the reader must reason about relationships, sequence, state, topology, branching, or dependencies. Prose explains a simple fact better.
2. Mermaid syntax is portable; renderer behavior is not. Treat the target renderer as a compatibility constraint.
3. Model before styling. Nodes, edges, labels, direction, and boundaries come first.
4. Verify the target renderer and version before using version-sensitive syntax.
5. If no renderer is available, say the diagram is unrendered rather than implying it was checked.
6. Keep diagrams small enough to read. Split at roughly 10 to 15 entities rather than shrinking the font.
7. Never send proprietary architecture, credentials, or personal data to an online renderer.
8. No em dashes in diagram labels or surrounding documentation.

## Authorization model

| User instruction | Authorized scope |
| --- | --- |
| "diagram this" | Produce the Mermaid block for the named structure |
| "add a diagram to the README" | The diagram plus the surrounding explanation the file needs |
| "check if this renders" | Render it, if a renderer is already available |
| "install Mermaid CLI and check" | A separate authorization that covers installing the tool |
| "put this in the online editor" | Only after naming the content being sent, and never for confidential material |

Installing a renderer, an icon pack, or Docker changes the environment and needs its own
authorization. Do not set one up implicitly to validate a diagram.

## Step 0: Decide whether a diagram earns its keep

Use a diagram when the reader must reason about relationships, sequence, state, topology,
branching, or dependencies. Do not force a diagram onto a simple fact that prose explains
more clearly.

For persistent documentation, treat the target renderer as a compatibility constraint.

## Step 1: Choose the diagram type

Read `references/diagram-type-selection.md`. Match the diagram to the structure being modeled:

| Structure | Preferred type |
|---|---|
| Process or decision tree | Flowchart |
| Interactions over time | Sequence |
| Domain objects and relationships | Class or ER |
| Service architecture | C4 or architecture |
| Cloud and deployment topology | Architecture |
| Lifecycle | State |
| Repository history | Git graph |
| Schedule with dependencies | Gantt |
| Simple proportions | Pie or xychart |
| Work stages and handoff | Kanban |
| Packet layout by bit range | Packet |
| Set overlap | Venn |
| Cause and effect | Ishikawa |
| Hierarchy or brainstorm | Mindmap, treemap, or timeline |

Use a specialized diagram only when its semantics help the reader. For venn, ishikawa,
kanban, packet, radar, treemap, mindmap, timeline, journey, and sankey, read
`references/new-diagrams.md` first.

## Step 2: Establish compatibility

Identify the target renderer and Mermaid version when the diagram will live in a repository.
If the renderer is unknown, avoid syntax known to be version-sensitive and state the assumption.

Read `references/renderer-adapters.md` before using beta syntax, newer directives, themes,
or icon packs. Beta types require an explicit fallback or a pinned version for persistent docs.

## Step 3: Model before styling

Define nodes, edges, labels, direction, and boundaries first. Keep labels short and meaningful.
Use subgraphs or C4 boundaries to make ownership and system boundaries explicit.

Keep styling minimal until the structure is correct. Add color and layout only after the
relationships read clearly in plain form.

## Step 4: Validate

Read `references/validation-and-rendering.md`, `references/security.md`, and the diagram-type
reference as needed. Check:

- syntax parses in the target renderer,
- labels are unambiguous and quoted where needed,
- direction and edge semantics are correct,
- IDs are stable and unique,
- special characters are safely quoted,
- beta syntax has a fallback or pinned version when the doc is long-lived,
- the diagram is readable at its intended size,
- no secrets, credentials, or personal data are embedded.

If a renderer is available, render-test it. Otherwise perform static syntax checks and clearly
label the result as unrendered.

## Step 5: Deliver for the destination

For chat, provide the Mermaid block plus a short interpretation when useful. For README/wiki/PR
content, preserve the exact fenced block and any required surrounding explanation.

## Failure handling

When a diagram does not render or a target rejects it:

1. report the actual parser or renderer error rather than describing the intended appearance
2. check the diagram-type keyword against the relevant reference, since a typo fails loudly instead of degrading
3. check config and theme option names, because unrecognized options are usually ignored silently, so a diagram can appear to render while the intended style was never applied
4. simplify by splitting the diagram, not by shrinking the text
5. if the target renderer lacks the required feature, say so and offer broadly supported syntax
6. never claim a diagram was rendered when it was only linted

A clean exit with an output file means the syntax parsed. Anything else means fix it before
presenting the diagram as finished.

## Anti-patterns

- Assuming Mermaid support is identical across platforms.
- Using new or beta syntax without checking renderer and version support.
- Using beta diagrams in long-lived docs without a fallback or pinned version.
- Turning every paragraph into a diagram.
- Overloading nodes with prose.
- Encoding secrets, credentials, or real personal data into examples.
- Claiming a diagram was rendered when it was only linted.
- Inventing keywords, config keys, or version support from memory.
- Using em dashes in documentation.

## Bundled references

Load `references/diagram-type-selection.md`, the chosen diagram-type reference, and any advanced
feature reference needed for the requested syntax:

- `references/diagram-type-selection.md`: decision guide for choosing the right diagram type based
  on what is being modeled.
- `references/flowcharts.md`: flowchart syntax, structure, and common patterns.
- `references/sequence-diagrams.md`: sequence diagram syntax, actor/participant patterns, and
  common idioms.
- `references/class-diagrams.md`: class diagram syntax, relationships, and common patterns.
- `references/erd-diagrams.md`: ER diagram syntax, cardinality, and common patterns.
- `references/c4-diagrams.md`: C4 model syntax, context/container/component boundaries, and common
  patterns.
- `references/architecture-diagrams.md`: architecture diagram syntax, cloud/deployment topology, and
  common patterns.
- `references/misc-diagrams.md`: state diagrams, git graphs, gantt charts, and pie/bar charts.
- `references/new-diagrams.md`: kanban, packet, venn, ishikawa, radar, treemap, mindmap, timeline, journey, sankey, and other specialized types with version minima and beta rules.
- `references/security.md`: secrets, personal data, injection risks, and safe validation boundaries.
- `references/advanced-features.md`: newer syntax, directives, themes, and version-sensitive
  features.
- `references/renderer-adapters.md`: target renderer and version compatibility checks.
- `references/validation-and-rendering.md`: how to validate diagrams before delivering, common
  pitfalls, export options, and where diagrams render without export.
- `references/proactive-trigger.md`: when to reach for a diagram without being asked, and when to
  stay quiet.
- `references/verification-and-failure.md`: shared verification and failure-handling principles.
