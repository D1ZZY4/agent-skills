# Report Format

Every deep research report follows the same shape so findings stay comparable
across audits. Short reports keep every section; they just keep each one brief.

## Shape

1. **Verdict first.** One paragraph: what was audited, the overall judgment, and
   the count of HIGH findings. If there are zero HIGH findings, say so.
2. **Methodology.** What was read in full (file counts), what was fetched live
   (named sources), the resolved mode (for auto, write "auto -> X") and whether it
   is a depth or specialized mode, and the material assumptions the work rests on.
   No checked-looking claims about unchecked work.
3. **Strengths.** What verified as correct and current, with the source that
   confirms each. This is evidence, not praise.
4. **Findings by severity.** HIGH first, then MEDIUM, then LOW. Each finding:
   the claim, the source that contradicts or confirms it, and the concrete fix.
5. **Claim ledger.** A compact table of every load-bearing claim with its grade
   and sources, so nothing verified mid-audit goes missing from the record:

   | Claim | Grade | Sources |
   |---|---|---|
   | DIALECT 1 remains the server default | Verified | redis.io dialects page (fetched), Context7 snippet |
   | All four README URLs live | Verified | four raw fetches (dates recorded in the report) |
6. **Remaining gaps.** Honest leftovers: sampled-but-unverified items, paywalled
   sources, judgments that need a human call. Include a short counterevidence
   note: the strongest evidence found against the verdict, why it does not
   overturn it, and what would change that assessment.
7. **Recommendations.** Numbered, ordered by severity, each one actionable.
8. **Metadata footer.** Resolved mode, source count, fetch date, and validation status
   (which checklist items passed, which were waived and why), so a later
   reader can judge the report without rerunning it.

## Per-mode add-ons

Keep the base shape above in every mode. Add one block when the mode needs it:

- **Forensic:** timeline table with date, event, and source per link, plus a
  provenance note for conflicting links.
- **Comparative:** symmetry matrix. Rows are evidence categories, columns are
  candidates, cells carry grade plus source. State the asymmetry explicitly when
  a cell cannot be filled.
- **Adversarial:** falsification section. List what was attacked, what survived,
  what fell, and the queries or fetches behind each attempt.
- **Exhaustive:** coverage table. Rows are source classes, columns are target,
  status (met, waived, open), and key sources.
- **Decision:** decision matrix. Rows are requirements R1 to Rn, columns are
  options with per-cell evidence grades, then trade-offs, risks, and the numbered
  recommendation that follows from the matrix.
- **Spot, Standard, Deep:** no add-on, except Deep keeps the counterevidence note
  in Remaining gaps.

## Long reports

When the report outgrows one comfortable delivery, emit it section by section
instead of shrinking the content: one complete section per message or file
write, each passing `quality-checklist.md` on its own, bibliography assembled
last from the ledger. Never compress by truncating; compress by narrowing the
scope in Step 0 instead.

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
