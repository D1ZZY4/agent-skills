# Report Format

Use a stable structure so readers can compare research runs without guessing what was checked.

## Shape

1. **Executive conclusion.** State the research question, what the evidence establishes, what remains
   unresolved, and the count of material findings. Do not overstate certainty.
2. **Scope and methodology.** State files or targets read, source classes fetched, resolved mode, research
   date, exclusions, material assumptions, and stopping rule. Distinguish actual work from planned work.
3. **Verified facts.** Present the source-backed facts that anchor the conclusion.
4. **Findings.** Order by severity and impact. Each finding includes the claim, evidence state, source
   or locator, why it matters, and the concrete implication or fix.
5. **Claim ledger.** Compact table of load-bearing claims:

   | ID | Claim | State | Grade | Evidence |
   | --- | --- | --- | --- | --- |
   | C01 | Version gate | Verified | HIGH confidence | Official docs, release artifact |
6. **Counterevidence and remaining gaps.** State the strongest evidence against the current synthesis,
   unresolved claims, inaccessible sources, and what would change the conclusion.
7. **Recommendations.** Only when requested or clearly part of the task. Tie each recommendation to
   requirements, evidence, constraints, and trade-offs.
8. **Metadata.** Resolved mode, source count by origin, research date, relevant revisions, validation
   status, and any explicit waivers.

## Per-mode add-ons

- **Forensic:** timeline with date, event, source, revision, and provenance state.
- **Comparative:** symmetry matrix with the same evidence rows across candidates and explicit gaps.
- **Adversarial:** falsification log showing each attack category, query or fetch, and result.
- **Exhaustive:** coverage ledger showing every source class or candidate universe target as Met, Waived,
  or Open.
- **Decision:** requirement matrix with R1 to Rn, evidence per option, constraints, trade-offs, and
  recommendation traceability.
- **Deep:** one critique-round delta and resulting grade changes.
- **Code review:** use the aggregate shape from `code-review.md`, with Standards and Spec kept separate.

## Long reports

When the output exceeds a practical delivery size, split by complete sections. Do not replace missing
content with truncation markers. Assemble the claim ledger and bibliography only after all sections have
been verified.

## Tone

Clear, direct, technical, and neutral. Facts carry the argument. Use adjectives sparingly.

Avoid AI filler, essay signposting, and promotional language. Prefer:

> The current documentation lists X, while the checked release artifact contains Y.

over:

> Research shows that X is obviously the best modern approach.

No em dashes in the report.

## Forbidden content

- URLs that were never fetched successfully
- invented versions, flags, benchmarks, or compatibility claims
- certainty language that exceeds the recorded evidence state
- conclusions about files or candidates that were not actually inspected
- claims of complete coverage when the coverage ledger is open
