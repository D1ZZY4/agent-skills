---
name: deep-research-expert
description: >
  Plan and execute deep technical research, audits, and reviews: read a full scope before
  judging it, verify load-bearing claims against official docs, official repos, and community
  sources, grade evidence by strength, and deliver a severity-ranked report with explicit
  uncertainty. Trigger when the user asks for deep research, deep audit, deep review, or
  verification of a skill, library, or technical surface against its real sources.
license: SSPL-1.0
metadata:
  version: 1.0.0
  author: D1ZZY4
  priority: medium
---

# Deep Research Expert

## Purpose

Run deep technical research the way a careful reviewer works: read the entire scope first,
verify each load-bearing claim against its real sources, grade the evidence, and report
findings ranked by severity with uncertainty stated plainly. Breadth without verification
is not research; a narrow verified answer beats a wide guessed one.

## Step 0: Decide the depth and propose the plan

Not every question needs deep research. Use this skill when the user asks for a deep
audit, review, or verification, or when a claim could be wrong in a way that costs real
effort (wrong version gate, dead documentation link, invented API).

Before starting, state the plan compactly: scope (what will be read fully), sources
(official docs, repos, registries, community), and what counts as done. Wait for
confirmation when the scope is large or the research transmits sensitive context
outside the repository. Read `references/proactive-trigger.md` for when to offer
research without being asked.

## Step 1: Read the full scope first

Read every file in scope before judging any of it. Do not sample three files and write
conclusions about thirty. For local material, prefer full reads; for remote material,
fetch the page rather than trusting a search snippet. Record what was read so the
report's methodology section is factual, not aspirational.

## Step 2: Climb the source ladder

Verify against sources in strength order; weaker sources never overrule stronger ones
on the same claim. Read `references/source-ladder.md` for the ladder, when to use
each rung, and how to route library-specific lookups through `context7-expert`
instead of duplicating it.

## Step 3: Grade the evidence

Extract the load-bearing claims (version gates, URLs, command syntax, default values,
comparisons against upstream) and check each one. Read
`references/evidence-grading.md` for the verification rule, severity ranking, and
uncertainty labels. A single failed load-bearing claim outranks ten stylistic notes;
say so explicitly.

## Step 4: Deliver the report

Structure every report the same way so findings stay comparable across audits. Read
`references/report-format.md` for the shape, tone rules, and what must never appear
(an invented URL, an unverified version, a certainty claim over a single source).

## Safety boundary

Inspection is safe by default. Mutation is not.

- Read remote sources freely; never transmit secrets, tokens, personal data, or
  proprietary code in a query or fetch. Redact first or ask.
- Never present a fetched snippet, search excerpt, or training memory as a verified
  fact without checking the source it came from.
- Never invent URLs, versions, command flags, or compatibility claims. A link goes
  into a report only after its target was fetched successfully.
- Do not modify the audited subject (code, docs, versions) as part of the audit
  unless the user explicitly authorizes fixes as a separate step.

## Anti-patterns

- Sampling a few files, then writing "all files reviewed".
- Treating one search snippet as confirmation.
- Letting training memory overrule a live official source.
- Pasting links that were never fetched.
- Grading style nits and factual errors with the same severity.
- Expanding scope mid-audit without telling the user.
- Reporting "verified" for anything checked against a single weak source.
- Using AI filler ("delve", "leverage", "seamless") or essay signposting in the report.

## Bundled references

Load only the references needed for the current phase:

- `references/proactive-trigger.md`: when to offer deep research without being asked, and when to stay quiet.
- `references/source-ladder.md`: source classes in strength order, what each rung proves, and routing to `context7-expert`.
- `references/evidence-grading.md`: claim extraction, the two-source rule, severity ranks, and uncertainty labels.
- `references/verification-and-failure.md`: shared verification and failure-handling principles.
- `references/report-format.md`: report shape, professional tone rules, and forbidden content.
