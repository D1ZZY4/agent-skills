# Evidence Grading

How to turn raw findings into a trustworthy verdict. Grade claims, not vibes.

## Extract load-bearing claims first

Before verifying anything, list the claims whose failure would change the
conclusion: version gates, URLs, command syntax, default values, quantitative
comparisons ("3 skills", "10x faster"), and provenance statements ("official",
"deprecated", "removed"). Style observations are never load-bearing.

## The verification rule

- A load-bearing claim needs **two independent sources** where it matters
  (versions, syntax, defaults), or one live official source fetched directly.
- A search snippet alone verifies nothing; it only nominates a source to fetch.
- A fetch failure is data: record which URL failed and how, then find the claim
  another way instead of dropping it silently.

## Severity ranks

- **HIGH, factually wrong.** The claim contradicts its best source. Fix before
  anything else. Example: "removed" when the source says "deprecated".
- **HIGH, strategic gap.** A whole expected domain is missing (an upstream skill
  with no local counterpart, a data type with no reference). Ranks with factual
  errors because users act on the omission.
- **MEDIUM.** Stale links after a docs migration, missing version gates on true
  claims, unverified subcommand details, routing gaps between references.
- **LOW.** Wording polish, single filler words, historical notes that need one
  clarifying sentence.

One HIGH finding outweighs any number of LOWs. State that ordering in the
report so a clean style score never hides a broken fact.

## Uncertainty labels

Use exactly these, no synonyms:

- **Verified**: fetched live source agrees; name the source.
- **Partially verified**: one strong source, or strong but indirect evidence
  (for example, an API listing without page content).
- **Unverified**: training memory or a single weak source; do not act on it
  without a follow-up check.
- **Fetch failed**: the source could not be retrieved; record URL and error.

## Consistency sweep

After the main pass, grep the whole scope for the fixed claim's siblings: the
same wrong default restated in client examples, the old URL prefix in other
files, the old count in another section. One fix without its siblings is half
a fix.
