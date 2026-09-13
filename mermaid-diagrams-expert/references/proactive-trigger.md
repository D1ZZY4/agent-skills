# Proactive Trigger

When to reach for a diagram without being asked, and when to stay quiet. This skill targets
persistent, renderable Mermaid syntax; it is not a general-purpose inline chart tool.

## When to act

- **Explaining architecture or system structure**: describing how services, components, or
  modules relate. A paragraph like "the frontend calls the API, which calls the database, which
  then notifies the queue" is exactly the shape a diagram communicates faster and more precisely
  than prose.
- **Explaining a flow over time**: API request and response cycles, auth flows, and event
  sequences, anything where order and timing matter.
- **Explaining a database schema or data model**: table relationships, foreign keys, and
  cardinality. Prose descriptions of schemas are hard to follow; an ERD is not.
- **Explaining a decision process, algorithm, or user journey**: anything with branches,
  conditions, or a "then this happens, unless that happens" structure.
- **Designing or documenting a domain model**: classes, their attributes, methods, and how they
  relate through inheritance, composition, or association.
- **Onboarding, a README, a PR, or a design doc is coming**: these are the contexts where a
  diagram becomes living, version-controlled documentation instead of a one-off explanation
  that goes stale.
- **A plan or architecture is being discussed before implementation**: sketching the diagram
  first catches structural problems earlier and cheaper than catching them in code review.

## When to stay quiet

- The structure being explained is genuinely linear and simple enough that a diagram would add
  ceremony without adding clarity, for example three steps in a strict sequence with no branches.
- The user is asking a narrow, single-fact question where a diagram would be a non-sequitur.
- A diagram was already produced for the same structure earlier in the conversation, and nothing
  about that structure has changed. Do not regenerate it just to re-illustrate the same answer.

## How to offer

If the request is clearly asking for an explanation of a structure that benefits from a diagram,
produce the diagram directly. If it is more ambiguous whether a diagram is wanted alongside the
prose answer, a brief diagram can still accompany the explanation instead of being asked about
first: prose plus diagram is rarely worse than prose alone when the underlying structure
genuinely has entities and relationships.

## Inline chart tools

If the environment has a separate, general-purpose visualization tool for one-off inline
diagrams shown only in a chat interface, that tool and this skill overlap in capability but
serve different purposes. This skill produces diagrams meant to be saved, committed, and
rendered by GitHub, GitLab, Notion, or a documentation site: valid Mermaid syntax that keeps
working wherever it is embedded. When the target is a repo file, a PR description, a README, or
any other place where the Mermaid syntax itself will be read, this skill's output format (plain
Mermaid in a fenced code block or a `.mmd` file) is the right one to use.