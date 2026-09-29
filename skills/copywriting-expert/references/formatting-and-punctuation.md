# Formatting and Punctuation

Portable defaults for generated copy. Project-specific style guides, locale rules, and quoted source text take precedence.

## Em dash policy

This project preference avoids em dash U+2014 in generated UI copy.

When no project rule exists, prefer periods, commas, colons, or parentheses. Do not alter an exact quoted legal, language, product, or source string merely to satisfy this default.

Do not replace required ASCII hyphens in commands, flags, identifiers, paths, URLs, or version strings with typographic dash characters.

When a technical string contains Unicode punctuation, preserve it exactly when the string is an external contract.

## Sentence case

Use sentence case for UI controls, headings, labels, and menu items unless the project uses another documented convention.

Consistency matters more than a claim that one capitalization style is universally correct.

## Ellipses

Use an ellipsis when the project uses it to signal that an action opens another step or dialog, for example `Export...`. Do not use ellipses merely for dramatic pauses in functional UI copy.

Follow the project's Unicode convention for `...` versus `…`.

## Oxford comma

Treat the Oxford comma as a project and locale convention, not a universal law. Use it when the project style guide requires it or when it materially improves clarity.

## Exclamation points

Use sparingly. Reserve them for product moments where enthusiasm is intentional and appropriate. Routine status messages generally do not need one.

## Numbers

Do not apply a blanket "spell out 0 through 9" rule to every UI surface.

Use numerals when users need to scan a count, measurement, price, percentage, version, date, time, or other structured value. Use the project's prose convention elsewhere.

Always consider locale-aware formatting for numbers, currencies, dates, times, and units.

## Contractions

Contractions are fine when consistent with the project's register. High-stakes, legal, regulated, or formal copy may use uncontracted forms when that matches the project convention.

## Placeholders and markup

Treat placeholders, variables, interpolation syntax, Markdown, HTML, escape sequences, and CLI flags as structural data.

Examples that must remain intact unless the task explicitly changes them:

```text
{count}
{{projectName}}
${amount}
--output <path>
```

Do not translate variable names, alter shell syntax, or move markup across grammatical boundaries without checking the rendering and localization implications.

## Final Unicode check

Before finalizing generated copy, check for accidental non-ASCII punctuation in technical strings, invisible characters, mismatched quotation marks, and malformed interpolation syntax.
