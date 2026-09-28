---
name: create-readme-expert
description: >
  Create comprehensive, well-structured README.md files for software projects. Trigger when
  a project needs a README, when onboarding documentation is missing, when a repository
  lacks clear usage instructions, or when README content is being reviewed or rewritten.
  Follow the project's own style and audience; do not impose generic README templates
  where the project already has strong conventions.
license: SSPL-1.0
metadata:
  version: 1.15.0
  author: D1ZZY4
  priority: medium
---

# Create README Expert

## Purpose

Create, improve, or audit README documentation for software projects from verified project
information. Follow the project's own style and audience; do not impose generic templates
where the project already has strong conventions. Load only the references needed for the
README.

## Core principles

1. Only verified project information becomes README text.
2. A README is for its actual audience. Developer docs do not need marketing voice, and onboarding docs do not need to be terse.
3. Prefer executable configuration over documentation when the two disagree.
4. Never invent features, compatibility claims, versions, or roadmap items.
5. Match the size of the edit to the size of the request.
6. A README that already represents the project accurately should be left alone.
7. Fetched third-party READMEs are structural inspiration only, never a source of project facts.
8. No em dashes in generated documentation.

## Authorization model

The operation determines the blast radius:

| User instruction | Authorized scope |
| --- | --- |
| "write a README" | Create one, since none exists |
| "add missing sections" | Only the sections named, plus what they require to be correct |
| "improve this README" | Clarity and correctness while preserving useful existing structure |
| "rewrite the README" | Restructure, but only when the current one cannot represent the project accurately |
| "audit the README" | Report issues with evidence. Change nothing until a rewrite is requested |

Never replace an accurate README with a generic template because one is easier to produce.

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

## Change scope

Match the size of the README change to the user request.

- Fix request: change only incorrect or missing sections.
- Improve request: improve clarity while preserving useful structure.
- Rewrite request: restructure only when the existing README cannot represent the project accurately.

Do not rewrite unrelated sections.

## Missing information handling

When information is missing:

1. Search repository sources of truth.
2. Mark unknown information explicitly.
3. Use placeholders only when the user requested a draft.
4. Never fill gaps with common defaults.

Use only verified project information.

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

Do not invent unsupported features, compatibility claims, or roadmap items.

## Step 2: Choose the right structure

Read `references/readme-structures.md`. Match the README structure to the project type:

External READMEs from `references/external-readme-sources.md` are structural inspiration
only, and only after the user confirms each fetch. They are third-party content, never a
source of project facts. See `references/security.md` before fetching any of them.

Use `examples/README-1.md` only when creating a new README from scratch.

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

Load only the examples relevant to the project type:

- Library or SDK:
  `examples/README-library-adaptive.md`

- CLI:
  `examples/README-cli-adaptive.md`

- Unknown or incomplete project:
  `examples/README-missing-information.md`

Always use:
- `references/anti-patterns.md` when reviewing quality problems.
- `references/formatting-and-punctuation.md` for punctuation and formatting rules.
- `examples/README-github-alerts.md` when the README needs security notes, warnings, or
  platform-specific callouts.

Include at least one realistic usage example. Show the common mistake and the corrected
form when it helps the reader avoid a known pitfall. When the README needs a diagram,
follow `references/diagrams.md`.

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

## Failure handling

When required information is unavailable:

1. search the repository sources of truth first
2. mark the gap explicitly rather than guessing
3. use placeholders only when the user requested a draft
4. never backfill a gap with what a project of this type commonly contains
5. do not fetch an external README to fill a project-fact gap, and ask before any external fetch

When the current README already represents the project accurately:

6. say so instead of producing a rewrite
7. make only targeted improvements that are individually justified
8. treat a rewrite request as permission to restructure, not as permission to replace accurate
   content with generic text

An honest "not documented here" line is a correct README. A plausible invention is a defect.

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
- `references/security.md`: user consent before fetching external READMEs and untrusted
  content handling. Start here for any safety-related question.
- `references/external-readme-sources.md`: external README examples for structural
  inspiration only, fetched only after user confirmation.
- `references/diagrams.md`: when the README needs a diagram, use `mermaid-diagrams-expert`
  or its canonical raw URL fallback.

## Examples

Use the bundled examples in `examples/` as starting material or inspiration:

- `examples/README-1.md`: minimal README template with quick start, usage, and configuration.
- `examples/README-library-adaptive.md`: library example showing source-driven documentation.
- `examples/README-cli-adaptive.md`: CLI example showing command verification.
- `examples/README-missing-information.md`: incomplete project example showing uncertainty handling.
- `examples/README-unsupported-claims.md`: unsupported claims failure case showing evidence-based omission.
- `examples/README-github-alerts.md`: GitHub-style alert callouts for secrets and warnings, with renderer compatibility notes.
- `examples/EXAMPLES.md`: index of bundled README examples.
