# Depth Modes

Match the effort to the stakes. Pick one mode in Step 0 and state it in the
plan; changing modes mid-audit restarts the stopping rule, so choose honestly
up front.

| Mode | Phases run | Use when |
|---|---|---|
| Spot | Read scope, verify the single disputed claim, report | One URL, one version gate, one "is this true" question |
| Standard | Full Steps 0-4, one pass, no critique loop | Most audits and reviews; the default |
| Deep | Standard plus the critique loop in `critique.md` | High-stakes claims, pre-release material, anything presented as authoritative |

Rules for all modes:

- Spot mode still grades its one claim; a fast answer is not an ungraded one.
- Standard mode runs each phase once, in order. No revisits without switching
  to Deep.
- Deep mode adds exactly one critique round with delta queries, then delivers.
  Never an open-ended cycle; the loop has one iteration by construction.
- Name the mode in the report methodology so the reader knows what rigor the
  verdict carries.
- Switching up (Spot to Standard, Standard to Deep) keeps graded findings and
  runs only the ungraded scope; switching down drops the critique loop and
  marks loop-dependent grades as Partially verified.

## Outline check (Standard and Deep)

After grading and before reporting, compare the findings against the plan:
promote unexpected but evidenced angles, demote sections the evidence did not
support, and reorder by evidential strength. Restructure at most half the
outline; beyond that the scope was wrong, not the structure. Never add a
section with no evidence already in hand, and never drift into a different
question. Record what changed and why in the methodology.
