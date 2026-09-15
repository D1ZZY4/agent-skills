# Code Review as Deep Research

Review the changes since a caller-supplied fixed point along two deliberately
separate axes: Standards (does the code follow this repo's documented rules?)
and Spec (does the code implement what was asked?). The axes run independently
and report side by side; one axis never masks the other. Use for branch, PR,
or work-in-progress review, or whenever the user says "review since X". Not
for single-file typo checks or questions answerable from the diff alone.

## Step 1: Pin the fixed point

The fixed point is whatever the user named: a commit SHA, branch, tag, `main`,
or a relative ref such as `HEAD~5`. If none was given, ask before proceeding.

```bash
git rev-parse <fixed-point>
git diff <fixed-point>...HEAD
git log <fixed-point>..HEAD --oneline
```

Use the three-dot diff so the comparison runs against the merge-base. Confirm
the ref resolves and the diff is non-empty here; a bad ref or empty diff fails
now, not halfway through the review. If the diff is huge (hundreds of files or
several thousand lines), ask the user to narrow the scope first: one area, one
commit range, or the riskiest paths. Reviewing everything thinly is worse than
reviewing the risky slice well.

## Step 2: Identify the spec source

Find what the change was supposed to implement, in this order:

1. Issue references in commit messages (`#123`, `Closes #45`), resolved through
   the project's own issue workflow.
2. A path the user passed directly.
3. A spec file under `docs/`, `specs/`, or similar matching the branch or feature.
4. If nothing turns up, ask the user. If there is genuinely no spec, skip the
   Spec axis and report "no spec available" instead of inventing one.

## Step 3: Identify the standards sources

Collect every repo document that states how code should be written
(`CONTRIBUTING.md`, coding standards, agent rule files). Project rules win over
everything below.

On top of those, carry a fixed smell baseline for repos that document little:
common Fowler-style heuristics, each a labelled judgement call, never a hard
violation. Skip anything the toolchain already enforces (linters, formatters,
type checks); the review adds nothing by repeating them.

| Smell | What to look for | Fix direction |
|---|---|---|
| Mysterious Name | A name that does not reveal what the thing holds or does | Rename; no honest name means murky design |
| Duplicated Code | Same logic shape in more than one hunk or file | Extract once, call from both |
| Feature Envy | A method using another object's data more than its own | Move the method onto the envied data |
| Data Clumps | The same fields or params travelling together | Bundle into one type |
| Primitive Obsession | A primitive standing in for a domain concept | Give the concept its own small type |
| Repeated Switches | Same switch or if-cascade recurring on one type | Polymorphism or one shared map |
| Shotgun Surgery | One logical change scattered across many files | Gather what changes together |
| Divergent Change | One module edited for unrelated reasons | Split by reason |
| Speculative Generality | Abstraction for needs the spec never states | Delete until a real need shows |
| Message Chains | Long `a.b().c()` walks the caller should not know | Hide behind one method |
| Middle Man | A unit that mostly delegates onward | Cut it, call the target directly |
| Refused Bequest | A subtype ignoring most of what it inherits | Prefer composition |

## Step 4: Run the two axes

Run Standards and Spec as independent passes so neither pollutes the other.
With sub-agent support, spawn both in parallel with the diff, the commit list,
and their respective sources; without it, complete one axis fully before
starting the other.

- **Standards pass.** Per file or hunk: every breach of a documented standard
  (cite file plus rule), plus any baseline smell (name it, quote the hunk).
  Documented breaches can be hard violations; smells stay judgement calls; a
  documented repo rule overrides the baseline wherever they conflict.
- **Spec pass.** Missing or partial requirements, behaviour nobody asked for
  (scope creep), and requirements that look implemented but wrong. Quote the
  spec line behind each finding.

For high-stakes reviews, add one critique round: re-run the weakest axis with
delta queries against the gaps found, then stop. One loop, not an open-ended
cycle.

## Step 5: Aggregate without merging

Present the two reports under `## Standards` and `## Spec` headings, then one
summary line per axis: finding count plus the worst issue within that axis.
Never pick a single winner across axes and never rerank findings into one
list; the separation exists because a change can pass standards while failing
the spec, or the reverse.

Grade review findings with the labels in `evidence-grading.md`. A finding that
quotes both the offending hunk and the violated rule (or spec line) is
Verified; a smell with no repo rule behind it stays a judgement call.

## Sources checked

Concepts adapted (wording original) from two upstream skills:

- Two-axis review, fixed-point pinning, smell baseline:
  [mattpocock/skills code-review](https://raw.githubusercontent.com/mattpocock/skills/refs/heads/main/skills/engineering/code-review/SKILL.md)
- Depth modes, critique loop-back, claim-level verification discipline:
  [199-biotechnologies/claude-deep-research-skill](https://github.com/199-biotechnologies/claude-deep-research-skill)
