# Project-Specific Source of Truth

How to discover, prioritize, and apply project-specific content guidance without treating every existing string as automatically correct.

## What to look for

Inspect project-owned sources such as:

- content style guides
- design-system content documentation
- localization guidance and glossaries
- terminology files
- contribution or product-writing rules
- legal or compliance-approved language
- component documentation with copy conventions

Do not assume a specific path exists.

A targeted search can start with:

```bash
find . \
  \( -iname '*copywriting*' -o -iname '*content-style*' -o -iname '*voice-and-tone*' \
     -o -iname 'CONTENT_GUIDE.md' -o -iname 'STYLE_GUIDE.md' \
     -o -iname 'CONTRIBUTING.md' -o -iname '*glossary*' -o -iname '*terminology*' \) \
  -not -path './.git/*' \
  -not -path './node_modules/*' \
  -not -path './dist/*' \
  -not -path './build/*' \
  -print 2>/dev/null
```

Adapt the search to the repository's tooling and shell conventions. Do not modify files merely because the search finds them.

## Authority order

When guidance overlaps, prefer:

1. legally or contractually controlled wording
2. project-approved content and terminology guidance
3. locale-specific translation or terminology guidance
4. component and design-system conventions
5. established nearby product copy
6. portable defaults from this skill

If sources conflict, prefer the higher-authority source and note the conflict when it materially affects the result.

## Existing copy as evidence

Existing strings reveal real house terminology, but repetition does not prove correctness. Look for the same concept across several nearby surfaces before declaring a phrase established.

Watch for terms that are:

- overloaded across different concepts
- legacy names left for compatibility
- temporary implementation text
- copied from another product area with a different audience

## No documented style guide

Read enough of the README, docs, UI strings, and relevant flows to infer the local register and terminology.

Infer only what the evidence supports. Do not manufacture a brand personality, legal promise, accessibility behavior, or localization convention.

## Scope

A project style guide may cover only some surfaces. Apply its rules where they are actually specified, then use portable defaults for the gaps.

Do not turn the discovery process into a reason to rewrite unrelated copy.
