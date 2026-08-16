---
name: context7-expert
description: >
  Retrieve current, version-accurate documentation for libraries, frameworks, SDKs, APIs,
  CLIs, and cloud services through Context7 when authoritative, current documentation matters.
  Trigger for version-sensitive setup, configuration, API signatures, migration questions,
  dependency-specific code, or uncertainty about a named technology. Prefer project-local
  documentation and explicitly supplied versions when they are more authoritative. Do not
  invoke for library-independent programming concepts, ordinary refactors, or code whose
  correctness does not depend on external API behavior.
license: MIT
metadata:
  version: 1.7.0
  author: D1ZZY4
  priority: high
---

# Context7 Expert

This file is the routing and decision layer. Load only the reference needed for the current step.

## Step 0: Decide whether current documentation is actually needed

Use this skill when the answer could be wrong because an API, CLI, SDK, framework, service,
or version has changed. Strong triggers include a named dependency plus a concrete API question,
a version number, migration work, generated code against an external API, or uncertainty about
the current signature.

Do not use Context7 when:

- The question is about a general programming concept that does not depend on a specific library version (for example, "what is an array in JavaScript").
- The repository already contains the authoritative answer in local documentation, README, lockfiles, or manifests.
- The answer can be explained from stable, widely-known language semantics without consulting version-specific documentation.

Do not use documentation lookup as ritual. If the task is pure reasoning, refactoring, or
language syntax that does not depend on a third-party API, skip it.

## Step 1: Choose the strongest available source

Use this evidence order:

1. Repository-local documentation and lockfiles, when they define the project's actual version.
2. Official vendor documentation for that exact product and version.
3. Context7's indexed documentation for the requested library or platform.
4. Other primary sources only when the above are unavailable.

Never silently substitute a different major version because it is easier to find.

## Step 2: Choose the available Context7 mode

- **MCP available**: use the Context7 MCP tools. Read `references/mcp-mode.md`.
- **CLI available**: use the installed `ctx7` CLI. Read `references/cli-mode.md`.
- **Neither available**: read `references/risk-and-budget.md` before considering a network-backed fallback.
  Do not invent an installation state or execute an unapproved transient package command.

## Step 3: Resolve the technology precisely

Identify the product/library, ecosystem, and relevant version before querying. If the project
contains a lockfile or manifest, use it to constrain the lookup. If multiple similarly named
libraries exist, disambiguate before fetching docs.

## Step 4: Fetch narrowly and apply the result

Query for the exact task, not "everything about the library". Prefer primary API/reference
sections and version-specific migration notes. When documentation conflicts with memory,
trust the verified documentation.

When writing code, preserve the project's existing API style and dependency version. Do not
upgrade a dependency merely because newer documentation was found.

## Step 5: Report uncertainty honestly

If the source does not answer the question, say what was verified and what remains uncertain.
Do not fabricate a method, option, version, or compatibility claim.

## Anti-patterns

- Looking up documentation after already committing to an API from memory.
- Mixing examples from different major versions.
- Treating Context7 output as proof that the project has that dependency installed.
- Upgrading dependencies solely to make an example work.
- Querying broad documentation when one targeted reference would suffice.
- Claiming a tool was used when it was not available.

## Bundled references

- `references/proactive-trigger.md`: when to activate Context7 without waiting for the user to
  name it, the confidence threshold, and what not to narrate.
- `references/selection-and-query-writing.md`: how to pick the best library match and write good
  scoped queries.
- `references/mcp-mode.md`: MCP tool name variance, resolve/fetch mechanics, result handling, and
  error recovery.
- `references/cli-mode.md`: CLI command shape, resolve/fetch mechanics, version-specific IDs,
  optional flags, authentication, error handling, and common mistakes.
- `references/risk-and-budget.md`: operation budget tiers, when to increase budget, and rules for
  counting operations.
- `references/agent-adapters.md`: generic adapter contract, known examples, and portability rule
  for host-specific configuration.
- `references/setup.md`: setup modes, authentication, what gets written, and how to choose between
  MCP and CLI modes.
- `references/cli-skills-management.md`: install, search, suggest, generate, list, remove, and info
  commands for `ctx7` skills.
- `references/verification-and-failure.md`: verify the smallest controlling fact, prefer primary
  sources, distinguish checked from unchecked, safe static fallback, and never invent execution or
  compatibility.
