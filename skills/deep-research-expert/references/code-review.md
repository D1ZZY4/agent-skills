# Code Review as Deep Research

Review changes since a caller-supplied fixed point along two independent axes:

- **Standards:** does the change follow the repository's documented rules?
- **Spec:** does the change implement what the request or specification requires?

Neither axis may mask the other.

## Step 1: Pin the fixed point

The fixed point is the commit, branch, tag, or relative ref the caller supplied. If none is supplied,
the review is underspecified. Resolve the reference and establish the merge-base comparison before
reading findings.

```bash
git rev-parse <fixed-point>
git merge-base <fixed-point> HEAD
git diff <fixed-point>...HEAD
git log <fixed-point>..HEAD --oneline
```

Record whether the diff is empty, conflicted, unusually large, or based on an unexpected branch. Do not
rewrite or clean the tree merely to make the review easier.

## Step 2: Establish the specification

Find the intended behavior using this order:

1. issue, PR description, or task text explicitly tied to the change
2. user-provided specification or acceptance criteria
3. repository spec or feature document
4. commit message references resolved through the repository's issue workflow

If no specification can be established, run only the Standards axis and report the Spec axis as
"no spec available". Never invent requirements from coding style.

## Step 3: Establish standards

Read the repository's actual contribution rules, agent instructions, lint configuration, typecheck
configuration, test conventions, and relevant architectural documentation.

Tool-enforced rules should be verified by the tool rather than reclassified as reviewer taste. Human
review may still report design smells, but label them as judgement calls.

## Step 4: Inspect the change and context

Review the complete changed hunks and the surrounding code needed to understand behavior. Inspect tests,
configuration, generated artifacts, dependency changes, and call sites when they affect the claim.

Check for:

- correctness and edge cases
- security and data handling
- API or compatibility changes
- error and failure paths
- tests or missing tests where behavior requires them
- unrelated behavior changes
- documentation drift
- performance regressions when evidence supports the concern

## Step 5: Run the two axes independently

**Standards pass:** cite the repository rule and the changed code. Smells are judgement calls unless a
repository rule makes them mandatory.

**Spec pass:** map each material requirement to code evidence. Report missing, partial, incorrect, or
out-of-scope implementation without converting style preferences into spec failures.

For high-stakes reviews, run one critique round over the weaker or more consequential findings.

## Step 6: Verification

Where the environment permits and the task scope calls for it, run relevant checks such as tests,
typechecks, linters, builds, or focused reproductions. Record exact commands and outcomes.

A review can identify a likely defect without executing code, but then the result remains a static
finding, not a tested runtime result.

## Step 7: Aggregate without merging

Report:

## Standards

Findings ordered by severity, with rule citations.

## Spec

Findings ordered by severity, with requirement citations.

Then provide one summary sentence for each axis. Never choose a single overall winner between Standards
and Spec.

## Review boundaries

- Do not mutate the reviewed code during the review phase.
- Do not use `git restore`, `git clean`, reset, or history rewriting to simplify the review.
- Do not claim a test passed unless it was executed and observed.
- Do not infer missing requirements from unrelated conventions.
- Do not use a smell baseline to override an explicit project convention.
