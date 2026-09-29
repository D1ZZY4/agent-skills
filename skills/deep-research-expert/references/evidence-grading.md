# Evidence Grading

Grade claims, not impressions. The evidence grade describes what the current evidence supports. It is
not a probability and must not be treated as one.

## Claim ledger

Before verification, assign an identifier to every load-bearing claim:

| ID | Claim | Importance | Source required | Result |
| --- | --- | --- | --- | --- |
| C01 | Exact version gate | High | Official docs or shipped artifact | Open |
| C02 | Project pins version X | High | Lockfile or manifest | Open |

Importance is about how much the claim changes the conclusion, not how dramatic the wording sounds.

## Evidence states

Use exactly these labels:

- **Verified**: the best available source directly supports the claim, with a recorded locator and
  sufficient context for the claim. For high-risk claims, meaningful independent corroboration may
  also be required by the mode.
- **Partially verified**: evidence supports only part of the claim, is indirect, or leaves a material
  scope or provenance limitation.
- **Unverified**: the claim is plausible or supported only by weak evidence, memory, or discovery output.
  Do not act on it as established fact.
- **Contradicted**: a credible source directly conflicts with the current claim. Preserve the conflicting
  evidence and resolve or report the conflict.
- **Fetch failed**: the intended source could not be retrieved. Record the failure and do not silently
  replace it with a different claim.
- **Not applicable**: the check does not apply to this claim or mode.

"Not found" is not an evidence state. Use Unverified unless a declared coverage method makes absence
meaningful.

## Verification threshold

Do not impose a universal two-source rule. Instead:

- One live, claim-appropriate primary source can be sufficient for a direct vendor or project fact.
- Add independent corroboration when the claim is high-impact, contested, quantitative, security-sensitive,
  historical, or otherwise likely to be wrong despite a primary source.
- If the only available evidence is indirect, mark the claim Partially verified.
- If two sources share the same origin, treat them as one for independence purposes.

## Severity

Use severity for findings, not evidence state:

- **HIGH, factual or safety-critical failure**: the claim is wrong in a way that can cause material
  breakage, security impact, invalid decision support, or misleading public documentation.
- **HIGH, strategic coverage gap**: a missing evidence class or target makes the requested conclusion
  materially unsupported.
- **MEDIUM**: stale source, incomplete version boundary, missing corroboration where it is materially
  useful, or a routing/coverage defect that can mislead without immediate severe impact.
- **LOW**: wording, minor provenance detail, or a non-load-bearing omission.

Severity and evidence state are separate. A low-severity finding can be Verified. A high-severity
finding can remain Unverified when the evidence needed to settle it is inaccessible.

## Fact, inference, and recommendation

- **Fact**: directly supported by cited evidence.
- **Inference**: a conclusion drawn from multiple facts. Label it as an inference and show the supporting
  chain.
- **Recommendation**: an action proposed from the facts, constraints, and stated user goals. Do not
  disguise a recommendation as a factual finding.

Never write "research shows", "experts believe", or similar collective language without naming the
sources or studies represented by that phrase.

## Quantitative claims

A number without context is often pseudo-precision. For each material quantitative claim, record as
available:

- metric and unit
- denominator or population
- baseline or comparator
- measurement conditions
- date or version
- source and methodology

Do not compare numbers measured under incompatible conditions without labeling the limitation.

## Mode add-ons

- **Comparative**: every candidate gets the same evidence categories. Missing cells become explicit gaps.
- **Decision**: every requirement traces to evidence for each relevant option. An untraced requirement blocks
  a fully supported recommendation.
- **Adversarial**: record each disconfirmation attempt. Surviving an attempt raises confidence but does
  not prove a universal claim.
- **Exhaustive**: grade the coverage ledger itself as Met, Waived, or Open and report every Open class.
- **Forensic**: every timeline link records origin, date, revision, and evidence state.

## Consistency sweep

After the main verification pass, search the scope for repeated versions of load-bearing claims: old
URLs, stale counts, duplicated defaults, contradictory compatibility text, and examples that preserve
the old behavior. One corrected statement with stale siblings is not a complete correction.
