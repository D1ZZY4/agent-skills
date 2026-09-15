# Proactive Trigger

When to offer deep research without being asked, and when to stay quiet. Research costs
time and network calls, so the offer must earn its keep.

## When to act

- The user questions whether something is accurate, current, or complete ("is this still
  true", "is this real", "check against the official docs").
- A claim carries version, URL, syntax, or compatibility risk: a wrong answer breaks a
  build, ships a dead link, or misconfigures production.
- A skill, guide, or doc set is about to be published, bumped in version, or presented
  as authoritative.
- The same surface has drifted before (an upstream repo restructured, a docs site
  migrated paths, a preview feature went GA).

## When to stay quiet

- The question is small, stable, and fully answerable from verified local material.
- The user asked for speed over certainty and accepted the risk explicitly.
- The same scope was audited earlier and nothing about it has changed; say so instead
  of re-running the work.

## How to offer

Name the scope, the sources, and the stopping rule in one short proposal: "I can deep
check the 14 links in this skill against the live docs and report dead ones. Proceed?"
For ambiguous scope, offer two depths (spot check vs full audit) and let the user pick.
