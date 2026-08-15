---
name: create-readme-expert
version: "1.1.0"
description: >
  Create comprehensive, well-structured README.md files for software projects. Trigger when
  a project needs a README, when onboarding documentation is missing, when a repository
  lacks clear usage instructions, or when README content is being reviewed or rewritten.
  Follow the project's own style and audience; do not impose generic README templates
  where the project already has strong conventions.
license: MIT
metadata:
  version: 1.1.0
  author: D1ZYY4
  priority: medium
---

# Create README Expert

This file is the routing and decision layer. Load only the references needed for the README.

## Step 0: Decide whether a README is actually needed

Use this skill when the repository or project lacks clear entry-point documentation, when
a new project needs onboarding material, or when README content is being reviewed for
clarity, completeness, or audience fit. Do not overwrite an existing README without
checking project-specific guidance first.

If no source-of-truth document exists, infer from the codebase, existing docs, package
manifest, and explicit user requirements. Do not invent features, guarantees, or roadmap
claims.

## Step 1: Inspect the project

Before writing, inspect:

- Package manifest or project metadata (`pyproject.toml`, `package.json`, `Cargo.toml`,
  etc.)
- Directory layout and entry points
- Existing docs, comments, or inline help text
- CI, deployment, or usage scripts
- License and authorship metadata

## Step 2: Choose the right structure

Read `references/readme-structures.md`. Match the README structure to the project type:

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

Read `references/examples-and-anti-patterns.md` and `references/formatting-and-punctuation.md`.
Include at least one realistic usage example. Show the common mistake and the corrected
form when it helps the reader avoid a known pitfall.

## Step 5: Verify before delivering

Check:

- headings describe actual sections
- code blocks use the correct language tag
- links are valid and point to the intended destination
- the README matches the project's actual state, not a desired future state
- no em dashes appear in the README
- no secrets, credentials, or real personal data are embedded in examples

If the README will be rendered in a specific platform, verify renderer compatibility.

## Anti-patterns

- Copying a generic README template without adapting it to the actual project.
- Claiming features, tests, or compatibility not present in the codebase.
- Using examples that depend on unavailable dependencies or services.
- Encoding secrets, credentials, or real personal data into examples.
- Using em dashes in generated README content.
- Writing installation instructions that contradict the project's own setup docs.

## Bundled references

Load only the references needed for the README:

- `references/readme-structures.md`: common README structures by project type, section
  ordering, and when to include or omit sections.
- `references/voice-and-tone.md`: tone guidance for README content, including when to
  use concise technical style versus warmer onboarding language.
- `references/examples-and-anti-patterns.md`: worked good/bad README examples and
  common pitfalls.
- `references/formatting-and-punctuation.md`: the em dash ban and other punctuation rules.
- `references/verification-and-failure.md`: verify the README against the actual codebase,
  distinguish checked from unchecked claims, and how to handle missing information.
- `references/proactive-trigger.md`: when to propose, rewrite, or audit a README without
  being asked, and when to stay quiet.
