# Research Modes

Match effort to stakes and scope. `auto` selects the narrowest adequate mode. A mode is defined by
its question, evidence threshold, query pattern, reporting add-on, and stopping rule. It is not a
promise of a fixed token count or elapsed time.

## Auto

| Request signal | Mode |
| --- | --- |
| One defined claim, URL, version gate, or factual check | Spot |
| General audit, library research, documentation verification | Standard |
| High-stakes or authoritative claim, pre-release material | Deep |
| Incident, regression, historical reconstruction, disputed chronology | Forensic |
| Security, production readiness, controversial claim, explicit challenge | Adversarial |
| Full repo audit, landscape scan, literature survey, every qualifying candidate | Exhaustive |
| Controlled A versus B comparison | Comparative |
| Selection, migration, build versus buy, requirements with trade-offs | Decision |
| Fixed-point branch, PR, or work-in-progress review | Code review flow in `code-review.md` |

When multiple signals apply, choose one primary mode and name secondary lenses. Do not silently combine
separate full investigations.

## Spot

Focus on one defined claim.

Stopping rule: stop when that claim is Verified, Contradicted, or Fetch failed with a clearly documented
limitation. One or two narrow retrievals are normally enough. No broad sweep beyond a small consistency
check.

## Standard

Normal one-pass rigor.

Stopping rule: complete the declared scope, claim ledger, source retrieval, grading, synthesis, and
quality checklist once. Do not reopen settled claims without new evidence.

## Deep

Standard plus exactly one critique round.

Use for high-stakes claims, pre-release material, or content presented as authoritative. Every material
HIGH finding must be re-tested by the critique personas in `critique.md`, then kept, downgraded, or cut
with the reason recorded.

## Forensic

Reconstruct what happened.

Start with chronology: commits, tags, release artifacts, changelogs, diffs, issue dates, and archived
docs. Preserve conflicting evidence rather than smoothing it into one story.

Stopping rule: stop when remaining timeline gaps cannot change the conclusion, or explicitly record the
gaps and what evidence would close them.

## Adversarial

Try to falsify the conclusion.

Use when the user wants a security, readiness, safety, correctness, or contested claim challenged.

Stopping rule: run the declared falsification categories once, followed by the single critique pass if
specified by `critique.md`, then stop. Do not keep searching until a favorable result appears.

## Exhaustive

Measure coverage across a defined target set.

Declare source classes, candidate universe, versions, and exclusion rules before retrieval. Build a
coverage ledger. Breadth comes before deep inspection of individual items.

Stopping rule: every declared coverage target is Met, explicitly Waived, or Open. Never call a sample
"complete" because it was large.

## Comparative

Controlled comparison across candidates.

Use the same evidence categories, source classes, query templates, and version basis for each candidate.
Fill the matrix row by row across candidates.

Stopping rule: every material category is filled or explicitly marked as a gap for every candidate.
Do not manufacture symmetry when the evidence is genuinely asymmetric.

## Decision

Decision-ready synthesis for a stated set of requirements.

Start with requirements R1 to Rn and constraints. Trace each requirement to evidence per option, then
record trade-offs, risks, and unresolved gaps.

Stopping rule: all material requirements are traced, or untraced requirements are explicitly recorded.
A recommendation is allowed only as a synthesis from the stated requirements and evidence. Avoid an
unsupported "best overall" claim.

## Mode transitions

Changing mode changes the stopping rule. Preserve existing claim grades where the evidence still applies.
When escalating, run only the additional work required by the new mode. When downgrading, mark any
loop-dependent conclusion as no longer fully verified.

Switching into a specialized mode adds its required matrix, timeline, or coverage ledger without
re-reading already stable evidence unless the new mode needs it.

## Outline check

For all modes except Spot, compare the planned report against the evidence before delivery:

- add an evidenced issue that materially changes the answer
- remove unsupported sections
- reorder by evidence strength and severity
- do not add a section solely because it sounds useful

If more than half the report structure must change, record that the original research framing was
insufficient rather than silently pretending the plan was followed.
