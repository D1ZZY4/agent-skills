# Proactive Trigger

Offer research when verification materially reduces the risk of a wrong answer. Do not offer it merely
as a generic quality upgrade.

## Trigger conditions

- The user asks whether a claim is current, accurate, complete, or real.
- A statement depends on a version, URL, API shape, compatibility boundary, pricing, deprecation, or
  current release state.
- A skill, guide, architecture note, or technical document is about to be published or treated as
  authoritative.
- A source has recently migrated, been replaced, or shown signs of drift.
- A branch, PR, or work-in-progress needs a fixed-point review against a spec.
- The user compares candidates or asks for a selection. Use Comparative or Decision rather than an
  unstructured deep dive.
- An incident, regression, or disputed history requires reconstruction.
- The user asks for a security, readiness, safety, or controversial claim to be challenged.
- The user explicitly requests full coverage.

## Stay quiet when

- The question is small, stable, and answerable from verified local material.
- The user explicitly prefers speed and accepts the resulting verification limit.
- The same scope was recently audited and a current evidence basis shows no material change.
- External retrieval would require transmitting confidential material that has not been authorized.

## Freshness rule

Do not assume that a prior audit is still current merely because the URL is unchanged. Reuse prior work
only when its source revision, retrieval date, and the task's freshness requirement make that reuse valid.
Otherwise, verify the load-bearing portion again.

## How to offer

State the scope, likely mode, source classes, and stopping rule in one compact proposal. Avoid promising
an unbounded investigation. Example:

> I can verify the current CLI behavior against the official docs and shipped release, then report any
> mismatch in Spot mode. The run stops after the claim is resolved or the source fetch fails.

For large or sensitive work, state the transmission boundary and approval requirement before retrieval.
