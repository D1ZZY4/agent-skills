# Project-Specific Source of Truth

How to find and apply project-specific copywriting conventions before falling back to portable
defaults. Explains what to look for, where to look, and how to resolve conflicts between project
guidance and this skill's defaults.

## Why this matters

Some projects already have a design system with its own documented voice, tone, and copy
patterns. The original version of this skill was built entirely around one such file
(`apps/design-system/content/docs/copywriting.mdx`), which meant it did nothing useful in any
project that didn't happen to have that exact file at that exact path. This skill now works
natively everywhere by default, but a project's own documented conventions should still win
when they exist, since they reflect decisions already made and agreed on for that codebase.

## What to look for

Before applying the general defaults in the rest of this skill, check for a project-specific
content style guide in likely locations:

```bash
find . \
  \( -iname "*copywriting*" -o -iname "*content-style*" -o -iname "*voice-and-tone*" \
     -o -iname "CONTENT_GUIDE.md" -o -iname "STYLE_GUIDE.md" \
     -o -iname "CONTRIBUTING.md" \) \
  -not -path "./.git/*" \
  -not -path "./node_modules/*" \
  -not -path "./dist/*" \
  -not -path "./build/*" \
  -print 2>/dev/null
```

Common places these live:

- A design system package's docs folder (`apps/design-system/content/docs/`,
  `packages/ui/docs/`, or similar).
- A dedicated content style guide (`docs/content-style.md`, `CONTENT_GUIDE.md`).
- A section inside a broader contributing or style guide (`CONTRIBUTING.md`,
  `STYLE_GUIDE.md`).
- A host-specific agent rules or conventions file, if the project's agent integration documents
  one.

## If no style guide exists: read the project anyway

Even without a documented style guide, a project's existing code and docs are its de facto
copy standards:

- Read the README and any docs folders to learn the product's domain, terminology, and the
  register it already uses.
- Grep for existing UI strings (button labels, error messages, empty states) in the codebase
  and read a sample. These show the real house voice far more reliably than intuition.
- Identify the domain and audience: who reads this copy, and what vocabulary do they already
  use? A developer experience tool writes differently than a consumer finance app.
- Carry forward house terms verbatim. If the product already says "workspace", do not
  introduce "project space" for the same concept.

These de facto standards override portable defaults, exactly as a documented style guide would.

## How to apply it

- If a project-specific guide exists and addresses something directly (a specific tone
  decision, a house term for a feature, a specific error-message format), follow it exactly,
  it overrides the defaults in this skill's other reference files.
- If the project's guide is silent on something (it covers buttons but not empty states, for
  example), fall back to this skill's defaults for whatever it doesn't cover.
- If no project-specific guide exists at all, use this skill's defaults as-is, that's the
  normal case for most projects and nothing further is needed.
- Never assume a project has a specific guide without checking, and never skip checking just
  because a previous session in the same project didn't find one, conventions get added over
  time.
