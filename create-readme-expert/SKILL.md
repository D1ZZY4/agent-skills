---
name: create-readme-expert
description: >
  Create comprehensive, well-structured README.md files for software projects. Trigger when
  a project needs a README, when onboarding documentation is missing, when a repository
  lacks clear usage instructions, or when README content is being reviewed or rewritten.
  Follow the project's own style and audience; do not impose generic README templates
  where the project already has strong conventions.
license: MIT
metadata:
  version: 1.2.0
  author: D1ZYY4
  priority: medium
---

# Create README Expert

This file is the routing and decision layer. Load only the references needed for the README.

## Step 0: Identify the README operation

Classify the task before editing:

### Create
Use when no README exists. Build documentation from verified project information.

### Improve
Use when a README exists but contains missing, outdated, or unclear sections. Preserve useful existing structure and change only what needs correction.

### Audit
Use when reviewing README quality. Report issues and evidence before making changes unless rewriting is explicitly requested.

### Refuse unnecessary rewrite
If the README accurately represents the project, avoid replacing it with a generic alternative. Make only targeted improvements when they are justified.

If no source-of-truth document exists, infer from the codebase, existing docs, package
manifest, and explicit user requirements. Do not invent features, guarantees, or roadmap
claims.

## Step 1: Establish project sources of truth

Before writing, identify which files define the current project behavior. Inspect sources
in this priority order:

1. Explicit project documentation and contribution guidelines
2. Package manifests and build configuration (`pyproject.toml`, `package.json`,
   `Cargo.toml`, etc.)
3. Entry points, executable scripts, and public APIs
4. CI/CD, deployment, and release configuration
5. Existing README content that is still accurate
6. Comments, examples, and inline help text

If sources conflict:

- Prefer executable configuration over outdated documentation.
- Preserve project conventions unless they are clearly incorrect.
- Record uncertainty instead of guessing.

Do not invent features, guarantees, compatibility claims, or roadmap items when the
project sources do not support them.

## Step 2: Choose the right structure

Read `references/readme-structures.md` and `examples/README-1.md`. Match the README structure to the project type:

| Project type | Preferred emphasis |
|---|---|
| Library or SDK | Installation, quickstart, API overview, examples |
| CLI or tool | Installation, usage, flags, examples, configuration |
| Service or API | Endpoints, auth, request/response examples, deployment |
| Template or starter | What it includes, how to customize, prerequisites |
| Internal or enterprise | Setup, access, support, conventions |

A README should answer: what is this, who is it for, how do I start, and where do I go
next.

## Step 3: Write for the actual audience

Prefer specific verbs, plain language, active voice, and concrete examples. Keep the
primary action obvious. Avoid marketing fluff when the audience is a developer evaluating
or integrating the project.

For destructive or irreversible actions in examples, name the affected object and
meaningful consequence. For errors, explain the problem and next step when a next step
exists.

## Step 4: Add examples and anti-patterns

Read `references/anti-patterns.md`, `references/formatting-and-punctuation.md`,
`examples/README-1.md`, `examples/README-library-adaptive.md`,
`examples/README-cli-adaptive.md`, and `examples/README-missing-information.md`.
Use these as structural and tonal inspiration. Include at least one realistic usage
example. Show the common mistake and the corrected form when it helps the reader avoid
a known pitfall.

## Step 5: Verify before delivering

Check:

- headings describe actual sections
- code blocks use the correct language tag
- links are valid and point to the intended destination

For accuracy, safety, and missing-information rules, load the relevant
references instead of restating them here:

- `references/formatting-and-punctuation.md` for punctuation and formatting rules.
- `references/verification-and-failure.md` for claim verification and handling gaps.

If the README will be rendered in a specific platform, verify renderer compatibility.

## Anti-patterns

Loaded from `references/anti-patterns.md` and `references/formatting-and-punctuation.md`.
Do not duplicate them here; consult the references when auditing or writing.

## Bundled references

Load only the references needed for the README:

- `references/readme-structures.md`: common README structures by project type, section
  ordering, and when to include or omit sections.
- `references/voice-and-tone.md`: tone guidance for README content, including when to
  use concise technical style versus warmer onboarding language.
- `references/anti-patterns.md`: worked good/bad README examples and common pitfalls.
- `references/formatting-and-punctuation.md`: the em dash ban and other punctuation rules.
- `references/verification-and-failure.md`: verify the README against the actual codebase,
  distinguish checked from unchecked claims, and how to handle missing information.
- `references/proactive-trigger.md`: when to propose, rewrite, or audit a README without
  being asked, and when to stay quiet.

## Examples

Use the bundled examples in `examples/` as starting material or inspiration:

- `examples/README-1.md`: minimal README template with quick start, usage, and configuration.
- `examples/URL.md`: list of README sources for direct URL-based reference.
- `examples/EXAMPLES.md`: index of bundled README examples.
