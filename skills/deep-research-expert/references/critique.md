# Critique Loop

One adversarial pass over a finished draft, used by Deep mode and extended by
Adversarial mode (see `depth-modes.md`). The loop re-attacks the weakest findings
with delta queries, then the audit delivers. One iteration maximum. Forensic and
high-stakes reviews may borrow the same loop; Spot, Standard, Comparative,
Exhaustive, and Decision do not run it unless the plan explicitly escalates to Deep
or Adversarial.

## The three personas

Run each persona against the draft findings, not against the raw scope:

- **Skeptic.** Asks for the missing control: which rival explanation fits the
  same evidence, which claim rests on a single source wearing two hats.
- **Adversary.** Tries to break the verdict: the counterexample, the version
  where the claim fails, the URL that moved.
- **Implementer.** Asks what happens on contact with reality: which
  recommendation costs more than stated, which step assumes access nobody has.

## Delta queries

Each persona output must end in concrete follow-up checks, phrased as
retrieval tasks ("fetch the 8.x migration notes for the DIALECT default",
"confirm the alias list in the current CLI help"). Run them, fold the results
into the findings, and re-grade anything they touch. Findings that survive all
three personas keep their grade; findings that fall get downgraded or cut,
with the reason recorded.

## Falsification checklist (Adversarial mode)

Deep runs the personas once against the draft. Adversarial adds an active hunt
for disconfirmation before the personas close:

- contradictory evidence (sources that state the opposite)
- negative evidence (absence where presence is claimed)
- edge cases and known failures (open issues, incidents, breaking changes)
- competing explanations that fit the same evidence
- source incentives, bias, or single-origin repetition across sites

Each item needs a query or fetch on record. A verdict of "safe", "ready", or
"best" without a failed falsification attempt stays Partially verified at best.

## Stopping rule

The loop ends after one pass regardless of outcome, in Deep and in Adversarial. Leftover doubts become
Remaining gaps in the report, not a second loop. If the gaps cluster around
one claim, say which claim and what would settle it.
