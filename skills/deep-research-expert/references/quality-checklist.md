# Quality Checklist

Run this list over every report before delivering it. Each item is a concrete
check with a pass condition, not a vague aspiration. A report that fails any
item goes back for one fix round; a second failure stops delivery and becomes
a Remaining gaps entry instead of a silent pass.

## Completeness

- No truncation markers anywhere: "continues", "due to length", "sections X-Y",
  "additional sections", or any note explaining why part of the report is
  missing. A section is either complete or explicitly cut with its absence
  recorded in Remaining gaps.
- No placeholders: TBD, TODO, FIXME, "citation needed", "[8-75]"-style ranges,
  "etc." standing in for entries, or any promise that content "would be
  included".
- Every citation number in the body has a matching bibliography entry, and
  every bibliography entry is cited at least once. Numbering runs without gaps.

## Citation hygiene

- Every factual claim carries its citation in the same sentence, not three
  paragraphs later.
- Major claims cite independently: one source wearing two hats counts once.
- Fetched URLs resolve: spot-check that cited links load and point where the
  entry says. A dead link downgrades its claim, it never rides along silently.
- Years get a sanity pass: future years, pre-2000 sources cited for modern
  tooling, and recent claims with no verifiable source all get flagged.

## Fact versus synthesis

- Mark the boundary every time it appears. Facts read "according to [N]" or
  "[N] reports"; inferences read "this suggests" or "this implies".
- Never write "research shows", "studies suggest", or "experts believe" without
  naming who, with a citation attached.
- Speculation is allowed when labeled as speculation. Unlabeled speculation is
  a failed check.

## Density and shape

- Findings carry evidence in the same breath: numbers, quotes, or locators
  beside the claim, not in an appendix the reader must cross-reference.
- Bullets stay subordinate: lists enumerate, prose argues. A finding delivered
  entirely as bullets gets rewritten.
- Severity ordering holds: re-read the findings top to bottom and confirm a
  LOW never sits above an unresolved HIGH.

## Sources checked

Checklist discipline adapted (wording original) from the quality gates of
[199-biotechnologies/claude-deep-research-skill](https://github.com/199-biotechnologies/claude-deep-research-skill).
