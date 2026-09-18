# Research Modes

Match the effort to the stakes. Default mode is `auto`. Resolve it in Step 0 and
state the resolved mode in the plan; changing modes mid-audit restarts the stopping
rule, so choose honestly up front. A mode is not a token budget. Each mode below has
a different stopping rule, evidence requirement, query strategy, and reporting
add-on.

Architecture: depth chain runs Spot -> Standard -> Deep -> Forensic -> Adversarial
-> Exhaustive. Comparative and Decision are specialized modes, not deeper levels.
A specialized mode can borrow rigor from a depth level, but it reports with its own
shape from `report-format.md`.

## Auto (default)

Let the agent pick the best fit, then state it. Honor an explicit user-named mode
when given. Otherwise resolve by signals:

| Signals in the request | Resolve to |
|---|---|
| One URL, one version gate, one "is this true" question | Spot |
| General audit, review, library research, doc check, no comparison or decision asked | Standard |
| High-stakes claim, pre-release material, anything presented as authoritative | Deep |
| Incident, bug trail, disputed history, "why did this become like this", changelog or commit archaeology | Forensic |
| "A vs B", candidate list, alternative libraries, architectures, or tools | Comparative |
| "Is X production ready", security or compliance check, controversial claim, request to challenge a conclusion | Adversarial |
| "Cover all", landscape scan, full repo audit, literature or market survey, "find every implementation that meets constraints" | Exhaustive |
| "Which should we pick", build vs buy, migration, framework or vendor selection, requirements with trade-offs | Decision |
| Branch, PR, or work-in-progress review with a fixed point | Code review flow in `code-review.md`, rigor defaults to Standard |

If signals point two ways, pick the narrower mode first and note the secondary lens
in the plan. Example: "compare A vs B for a migration decision" resolves to
Comparative with a Decision matrix add-on, not two full runs. Auto never expands
scope silently; any expansion needs a new confirmation.

## Depth modes

### Spot: minimal effort, one defined question

- Focus: answer one claim with the minimum sufficient evidence.
- Use when: one URL, one version gate, one factual check.
- Stopping rule: stop when the single claim grades Verified or Fetch failed with a
  recorded fallback. No sweep for siblings beyond one grep.
- Evidence requirement: grade the one claim per `evidence-grading.md`. One live
  official source fetched directly is enough; otherwise two independent sources.
- Query strategy: one or two narrow fetches. No broad survey.
- Reporting: short form of `report-format.md`, all sections kept brief. Methodology
  names Spot and the single claim.

### Standard: normal rigor, one pass

- Focus: full Steps 0-4 once, in order.
- Use when: most audits and reviews; the default when auto has no stronger signal.
- Stopping rule: each phase runs once. No revisits without switching mode.
- Evidence requirement: two-source rule for load-bearing claims where it matters.
- Query strategy: scoped fetches per claim, parallel where the harness allows, per
  `source-ladder.md` retrieval discipline.
- Reporting: base shape in `report-format.md` with no mode add-on.

### Deep: critical verification

- Focus: Standard plus exactly one critique round.
- Use when: high-stakes claims, pre-release material, anything presented as
  authoritative.
- Stopping rule: one critique pass with delta queries from `critique.md`, then
  deliver. Never an open-ended cycle.
- Evidence requirement: as Standard, plus every HIGH finding must survive the
  three personas or be downgraded with a recorded reason.
- Query strategy: Standard fetches plus persona-driven delta queries against gaps.
- Reporting: base shape plus an explicit counterevidence note in Remaining gaps.

### Forensic: reconstruction

- Focus: what actually happened, based on the traceable trail.
- Use when: incidents, complex bugs, disputed claims, historical trails, API
  evolution, repo archaeology.
- Stopping rule: stop when the timeline has no unexplained gaps that change the
  conclusion, or record the remaining gaps with what would close them.
- Evidence requirement: chronological chain with provenance per link (commit,
  tag, changelog, release note, archived doc). Preserve contradictions instead of
  smoothing them. Prefer primary URLs over mirrors.
- Query strategy: version and history tracking first (tags, changelogs, diffs),
  then cross-check primary vs secondary. Establish the current date early.
- Reporting: base shape plus a timeline table (date, event, source) and a
  provenance note per key link. See `report-format.md`.

### Adversarial: falsification

- Focus: try to break the conclusion being built.
- Use when: production readiness, security or compliance validation,
  controversial claims, any "prove X is safe or best" request.
- Stopping rule: stop after the falsification checklist in `critique.md` is
  worked once (contradictory evidence, negative evidence, edge cases, known
  failures, competing explanations, source incentives). Leftover doubts become
  Remaining gaps, not a second loop.
- Evidence requirement: actively seek disconfirming sources. A verdict of "safe"
  or "best" needs failed falsification attempts on record, not just supporting
  sources.
- Query strategy: failure-first queries ("X failure", "X limitation", "X incident",
  open issues, breaking changes), then balance with supporting sources.
- Reporting: base shape plus a falsification section (what was attacked, what
  survived, what fell) and a strengthened counterevidence note.

### Exhaustive: coverage

- Focus: measurable coverage of a defined scope, not infinite depth per item.
- Use when: large repo audits, ecosystem or market scans, literature reviews,
  "find every X that meets constraints".
- Stopping rule: stop when the declared coverage targets are met or explicitly
  waived in Remaining gaps. Never claim full coverage from a sampled sweep.
- Evidence requirement: coverage ledger by source class (official docs, repos,
  registries, changelogs, issue trackers, independent sources). Deduplicate by
  origin; three pages quoting one announcement count as one.
- Query strategy: breadth-first across classes, then depth only on load-bearing
  items. Batch fetches in parallel, triangulate after.
- Reporting: base shape plus a coverage table (class, target, met or waived,
  key sources). Narrow the scope in Step 0 instead of truncating the report.

## Specialized modes

### Comparative: symmetry

- Focus: controlled comparison across candidates.
- Use when: product, library, architecture, or vendor comparisons.
- Stopping rule: stop when every candidate has the same evidence categories or
  the asymmetry is recorded as a gap. Never publish A with 17 sources and B with
  two random blogs as if that were a comparison.
- Evidence requirement: symmetry across categories (capabilities, limitations,
  architecture, performance, maintenance, licensing, deployment, ecosystem).
  Missing data is a finding, not a blank cell.
- Query strategy: same query template per candidate, same source classes per
  candidate. Fill the matrix row by row, not candidate by candidate.
- Reporting: base shape plus a symmetry matrix with per-cell grades and sources.
  No single "best" verdict without stated requirements; that synthesis belongs
  to Decision.

### Decision: synthesis for a choice

- Focus: turn evidence into decision-ready information without mixing fact and
  opinion.
- Use when: architecture choice, build vs buy, migration, tool or vendor
  selection.
- Stopping rule: stop when every requirement traces to evidence, constraints,
  trade-offs, and risks, or the untraced requirement is recorded as a gap.
- Evidence requirement: requirements first (R1 to Rn), then evidence per
  requirement per option. Facts carry citations; inferences read as inferences
  per `quality-checklist.md`.
- Query strategy: requirements-driven. Each requirement generates its own narrow
  queries; Comparative symmetry applies when options are compared.
- Reporting: base shape plus a decision matrix (requirement, weight if given,
  option scores with grades, trade-offs, risks) and numbered recommendations
  ordered by severity. Never write "X is best" without the matrix behind it.

## Rules for all modes

- Spot still grades its claim; a fast answer is not an ungraded one.
- Name the resolved mode in the report methodology so the reader knows what rigor
  the verdict carries.
- A weaker source never overrules a stronger one on the same claim; see
  `source-ladder.md`.
- One HIGH finding outweighs any number of LOWs; see `evidence-grading.md`.
- Switching up (for example Spot to Standard, Standard to Deep) keeps graded
  findings and runs only the ungraded scope; switching down drops loop-dependent
  work and marks loop-dependent grades as Partially verified.
- Switching into or out of a specialized mode restarts its add-on (symmetry,
  matrix, timeline, coverage, falsification) but keeps already graded claims.
- Code review tasks follow `code-review.md` Step 5 for the aggregate shape; the
  depth mode only sets the rigor.

## Outline check (all except Spot)

After grading and before reporting, compare the findings against the plan:
promote unexpected but evidenced angles, demote sections the evidence did not
support, and reorder by evidential strength. Restructure at most half the
outline; beyond that the scope was wrong, not the structure. Never add a
section with no evidence already in hand, and never drift into a different
question. Record what changed and why in the methodology. Comparative checks
symmetry here; Decision checks requirement traceability; Exhaustive checks
coverage targets; Forensic checks timeline gaps; Adversarial checks whether the
falsification pass moved any grade.
