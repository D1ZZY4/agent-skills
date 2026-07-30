# Message Style Rules

Full detail for Step 3 in SKILL.md.

## Format

```
<type>(<scope>): <short imperative summary>

<body, required, markdown>
```

## Subject line

- Scope is mandatory, not optional: `type(scope): summary`. Only skip the parentheses when
  the change genuinely touches the whole repo with no single module or area (a repo-wide
  dependency bump still gets `deps` as scope; a truly scope-less change is a rare exception,
  not the default).
- Pick the scope from the area actually changed: a module name, package, folder, feature, or
  component. Examples: `feat(api)`, `fix(auth)`, `docs(readme)`, `refactor(ui)`. Keep it
  short, lowercase, one word or short-hyphenated when possible.
- Imperative mood: "add", "fix", "remove", never "added", "adds", "adding"
- Short and punchy: aim 50 characters or less, soft cap around 72
- No trailing period
- No em dashes, ever. Not in the subject, not in the body, not anywhere in a commit message.
  Use a comma, colon, period, or parentheses instead.
- No en dashes either (Unicode U+2013, a shorter dash than an em dash but still not a plain
  hyphen), and no other smart-punctuation substitute for a plain ASCII hyphen (`-`) or double
  hyphen (`--`). This is not just a style preference: if a command-line flag like
  `--recurse-submodules` gets rendered with U+2013 in place of the two literal hyphens, the
  command is broken the moment someone copies and pastes it, it won't parse as the flag it
  looks like. Any literal shell command, flag, or path inside a commit message must use plain
  ASCII hyphens, always, no exceptions, double check any line containing `--` before it goes
  into the message.
- No emoji, ever. Not even if it seems fitting or the project uses them elsewhere.
- English only, always, regardless of the language the conversation is in

## Body: mandatory, always Markdown

- Every commit gets a body. Never subject-only, even for small changes. Explain the why at
  minimum, in a sentence or two, even if the what is obvious from the diff.
- Must use Markdown formatting: bullets (`-`), inline code, bold, headers all fine. A body
  that is a single unformatted sentence is fine content-wise, but reach for Markdown structure
  (bullets, code spans) whenever there is more than one point to make.
- Explain what and why, not how.
- Write it like a senior developer's commit, not a changelog or an AI status update. Don't
  enumerate every single file, asset, or doc that was touched as a checklist. Group related
  files into one bullet if they're the same concern (for example, "update 8 READMEs to point
  at the renamed LICENSE file" is one bullet, not eight). A body with more than about 4 to 5
  bullets is a sign the commit itself should have been split, not that the body needs more
  lines. If you catch yourself listing filenames one after another with no synthesis, stop and
  compress it into what actually changed conceptually.
- No em dashes, en dashes, or emoji in the body either. Same rules as the subject line.
- Wrap prose around 72 characters.
- Reference issues at the end when relevant: `Closes #42`, `Refs #17`.
- Breaking changes, security fixes, data migrations, and reverts always get a fuller body.
  Never compress these into a one-liner.

## Never include

- "This commit does X", "I", "we", "now", "currently"
- Inline prose like "As requested by..." or "Generated with X", use the `Co-authored-by`
  trailer instead (see below) rather than mentioning AI involvement in the subject or body
- Any emoji, under any circumstance
- Any em dash or en dash, under any circumstance
- The words `phase`, `session`, `iteration`, `step`
- Generic AI summaries like "Update documentation" or "Address findings from audit"

## AI co-author trailer

If the work was done with an agentic coding tool (Claude Code, Codex, Kimi, Gemini, or
similar) and that provider supplies an official noreply GitHub email for the agent, it's fine
to add a `Co-authored-by` trailer at the very end of the body, after everything else,
including any issue references. This is standard git practice, not an AI summary. Format
(illustrative only, use whatever real address the tool actually provides):

```
Co-authored-by: <agent name> <the agent's actual noreply address>
```

Rules for this trailer:

- **Exact format, no exceptions**: `Co-authored-by: Name <email>`. The casing is exactly
  `Co-authored-by`, lowercase `a` in "authored", lowercase `b` in "by", capital `C`. Not
  `Co-Authored-By`, not `CO-AUTHORED-BY`, not any other casing variant.
- **The email is always wrapped in angle brackets**, `<email>`, never bare. A trailer without
  the brackets is not a valid git trailer and won't be recognized as co-authorship by GitHub
  or git tooling, it'll just look like broken text sitting at the end of the commit.
- Wrong: `Co-Authored-By: Claude noreply@anthropic.com` (wrong casing, missing brackets)
- Right: `Co-authored-by: Claude <noreply@anthropic.com>`
- Only use an email the provider actually issued for this purpose, never invent one.
- It goes at the bottom, as its own line, after a blank line separating it from the rest of
  the body. Never woven into a sentence.
- Which tool gets credited, and in what exact name/email format, is up to whichever
  agent actually did the work. If multiple tools contributed, multiple `Co-authored-by`
  lines are fine.
- This trailer is the only acceptable place AI involvement shows up in a commit message.
  Nothing else in the subject or body should reference it.

## Commit type reference

| Type | When to use |
|------|-------------|
| `feat` | New feature or behaviour |
| `fix` | Bug fix |
| `chore` | Tooling, config, deps. No production code change |
| `docs` | Documentation only |
| `refactor` | Restructure without behaviour change |
| `style` | Formatting, whitespace. No logic change |
| `perf` | Performance improvement |
| `test` | Adding or fixing tests |
| `build` | Build system or dependencies |
| `ci` | CI configuration |
| `revert` | Reverting a prior commit |

Breaking change: append `!` after type/scope, explain in body with `BREAKING CHANGE: ...`.
