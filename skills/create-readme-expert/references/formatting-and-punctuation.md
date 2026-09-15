# Formatting and Punctuation

Rules for README formatting and punctuation.

## Em dash ban

Do not use em dashes in README content. Use commas, colons, periods, or parentheses instead.

## Code formatting

- Use fenced code blocks with a language tag.
- Do not wrap command examples in decorative ASCII boxes.
- Keep inline code short; prefer code blocks for multi-line examples.

## Headings

- Use sentence case unless the project standard requires title case.
- Keep headings descriptive and specific.
- Do not invent section hierarchy; the README should match the project's actual structure.

## Links

- Prefer absolute URLs for external links.
- Prefer relative paths for links within the repository.
- Do not link to files that do not exist.

## Callout blocks

- Use GitHub-style blockquote alerts for genuinely important notes: `> [!IMPORTANT]`,
  `> [!WARNING]`, `> [!CAUTION]`, `> [!NOTE]`, and `> [!TIP]`.
- Put the alert marker on its own line at the start of the blockquote, then one `>`
  before each content line.
- Reserve alerts for security notes, destructive actions, and common pitfalls. A plain
  paragraph is the default for everything else.
- Alert syntax is renderer-specific. Confirm the README's primary host supports it
  before relying on it; on unsupported platforms it renders as an ordinary blockquote.
- See `examples/README-github-alerts.md` for a worked example with secrets and warnings.
- Sources checked: GitHub alert types and syntax (NOTE, TIP, IMPORTANT, WARNING, CAUTION),
  https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax
