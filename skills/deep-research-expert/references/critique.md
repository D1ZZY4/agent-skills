# Critique Loop

One adversarial pass over a finished draft, available in Deep mode (see
`depth-modes.md`). The loop re-attacks the weakest findings with delta
queries, then the audit delivers. One iteration maximum.

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

## Stopping rule

The loop ends after one pass regardless of outcome. Leftover doubts become
Remaining gaps in the report, not a second loop. If the gaps cluster around
one claim, say which claim and what would settle it.
