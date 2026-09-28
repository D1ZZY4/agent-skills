# Proactive Trigger

When to offer deep research without being asked, and when to stay quiet. Research costs
time and network calls, so the offer must earn its keep. Default mode is auto; the
offer names the resolved mode from `depth-modes.md` plus its stopping rule.

## When to act

- The user questions whether something is accurate, current, or complete ("is this still
  true", "is this real", "check against the official docs").
- A claim carries version, URL, syntax, or compatibility risk: a wrong answer breaks a
  build, ships a dead link, or misconfigures production.
- A skill, guide, or doc set is about to be published, bumped in version, or presented
  as authoritative.
- The same surface has drifted before (an upstream repo restructured, a docs site
  migrated paths, a preview feature went GA).
- A branch, PR, or work-in-progress change is up for review, especially with a
  spec or issue to check against: load `code-review.md` and run its two-axis
  flow instead of a generic read-through.
- The user compares options (A vs B, library or architecture candidates): offer
  Comparative with a symmetry requirement, not a generic deep dive.
- The user must pick an option (build vs buy, migration, framework or vendor
  selection): offer Decision with a decision matrix.
- The user investigates an incident, regression, or disputed history: offer Forensic
  with a timeline and provenance chain.
- The user asserts production readiness, security, compliance, or a controversial
  best claim: offer Adversarial falsification.
- The user asks for full coverage (landscape scan, full repo audit, every candidate
  meeting constraints): offer Exhaustive with explicit coverage targets.

## When to stay quiet

- The question is small, stable, and fully answerable from verified local material.
- The user asked for speed over certainty and accepted the risk explicitly.
- The same scope was audited earlier and nothing about it has changed; say so instead
  of re-running the work.
- The offer would require transmitting confidential material, and the user has not approved sending
  it. Report what can be checked locally instead.

## Confidence rule

The offer must earn its keep. Offer research only when being wrong would cost real effort, for
example a wrong version gate, a dead documentation link, or an invented API.

Do not offer research as a general quality upgrade, and do not offer a mode heavier than the
question needs. Name the resolved mode and its stopping rule in the offer so the user can judge the
cost before agreeing.

## How to offer

Name the scope, the sources, the resolved mode, and the stopping rule in one short
proposal: "I can deep check the 14 links in this skill against the live docs and
report dead ones in Standard mode, one pass, no critique loop. Proceed?" For ambiguous
scope, name the auto pick plus one alternative (depth versus specialized) and let the
user pick. For review tasks, name the fixed point and the spec source before starting.
