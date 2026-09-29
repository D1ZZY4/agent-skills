# Verification and Failure Handling

Verification is an evidence state, not a tone of voice.

## Rules

- Verify the smallest fact that controls the decision.
- Use claim-appropriate primary sources and version-matched project evidence.
- Distinguish Not checked, Checked and passed, Checked and failed, Skipped, Not applicable, and Partial.
- Never invent execution results, compatibility, tests, installed tools, fetched URLs, or benchmarks.
- Record assumptions when they can change the conclusion.
- A failed retrieval changes the evidence state; it does not authorize substitution of a nearby source.
- A command failure is not automatically a product failure. Check environment, version, permissions,
  arguments, and the expected source before diagnosing the product.
- Absence claims require a declared search or coverage method that makes absence meaningful.
- Current claims require a date basis. Historical claims require a time boundary.
- Quantitative conclusions require enough methodological context to make the number interpretable.

## Failure classes

| Failure | Meaning | Required response |
| --- | --- | --- |
| Fetch failed | Intended source was inaccessible | Record URL and error; seek another source only if it can prove the same claim |
| Scope incomplete | Declared material was not fully read | Do not claim full coverage; record remaining items |
| Evidence conflict | Credible sources disagree | Preserve both and resolve by claim-specific authority, revision, and context |
| Query mismatch | Retrieved material does not answer the claim | Mark unresolved; refine query only within scope |
| Environment mismatch | Command or test ran under the wrong conditions | Re-run only after conditions are corrected and authorized |
| Provenance missing | Origin, revision, or date is unclear | Downgrade confidence and report the provenance gap |

## Failure recovery

After a failed check, first determine whether the operation had a side effect or partial result. Do not
blindly repeat a mutation or external request when state may already have changed.

When research fails, preserve the failed evidence path in the methodology. Do not erase the failure
just because another source later answered part of the question.

## Mode-specific reporting

- Exhaustive: report every Open coverage class.
- Comparative: report every asymmetry that affects interpretation.
- Decision: report every untraced material requirement.
- Forensic: report every timeline gap that could alter causality.
- Adversarial: report which falsification classes were actually attempted.

## No false completion

Never write "fully verified", "all checked", "production-ready", or equivalent language unless the
mode's completion rule and evidence requirements actually support it. A report can be complete as a
research artifact while still concluding that the underlying claim remains unresolved.
