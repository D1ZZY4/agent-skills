# Verification and Failure

How to verify a README against the actual project and how to handle missing information.

## Repository inspection checklist

Inspect when available:

- package manifests
- entry points
- executable scripts
- environment examples
- CI workflows
- deployment files
- public exports
- existing documentation

## Verify before claiming

- Run or read the code paths referenced in usage examples.
- Confirm installed dependencies, entry points, and CLI flags before writing them.
- Confirm URLs, repository names, and version badges before publishing them.

## Distinguish checked from unchecked

- State clearly what was verified directly.
- State clearly what remains uncertain or inferred from limited information.

## Handling missing information

- If a section cannot be written accurately, omit it rather than invent content.
- If the project is missing metadata, ask for it or mark it as a placeholder with a clear note.
- Never fabricate compatibility claims, performance numbers, or roadmap items.

## Safe fallback

- When the project state is unclear, default to a minimal README with project name, description,
  installation, usage, and license.
- Label assumptions explicitly rather than hiding them.
