# Report Format

Every deep research report follows the same shape so findings stay comparable
across audits. Short reports keep every section; they just keep each one brief.

## Shape

1. **Verdict first.** One paragraph: what was audited, the overall judgment, and
   the count of HIGH findings. If there are zero HIGH findings, say so.
2. **Methodology.** What was read in full (file counts), what was fetched live
   (named sources), and what was not checked. No checked-looking claims about
   unchecked work.
3. **Strengths.** What verified as correct and current, with the source that
   confirms each. This is evidence, not praise.
4. **Findings by severity.** HIGH first, then MEDIUM, then LOW. Each finding:
   the claim, the source that contradicts or confirms it, and the concrete fix.
5. **Remaining gaps.** Honest leftovers: sampled-but-unverified items, paywalled
   sources, judgments that need a human call.
6. **Recommendations.** Numbered, ordered by severity, each one actionable.

## Tone rules

- Clear, direct, developer-facing. No marketing filler, no cleverness where
  precision matters.
- Facts carry the weight; adjectives do not. Write "the page returns 404" not
  "the page is completely broken".
- Never use AI filler ("delve", "leverage", "seamless") or essay signposting
  ("It's important to note that"). The report documents its own anti-patterns
  by avoiding them.
- No em dashes in the report. Use commas, colons, periods, or parentheses.

## Forbidden content

- URLs that were never fetched successfully.
- Versions, flags, or compatibility claims from a single weak source.
- Certainty language over sampled or indirect evidence.
- Verdicts about files that were listed but never opened.
