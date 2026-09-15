# Source Ladder

Sources in strength order for technical claims. A weaker rung never overrules a
stronger one on the same claim. When two strong sources disagree, report both and
let recency plus authority decide, stated explicitly.

## The ladder, strongest first

1. **Live official documentation.** The vendor's current docs site (fetched, not
   snippeted). Proves: current syntax, version gates, deprecation status.
   Example: a command reference page showing `"since": "8.4.0"`.
2. **Official repositories and APIs.** Source files, release tags, package
   registries, machine-readable directory listings. Proves: what actually ships,
   file existence, exact structure. Example: a GitHub API listing proving a
   directory holds exactly three skills.
3. **Project-local evidence.** Lockfiles, manifests, changelogs, the checked-out
   code itself. Proves: what this project pins, uses, and claims. Always the
   authority for project-specific facts.
4. **Maintainer and community channels.** Release announcements, changelogs,
   maintainer blogs, issue threads. Proves: intent, timelines, known issues.
   Treat dates and promises as provisional.
5. **General web search.** Discovery only. A snippet is a pointer to a source,
   never the source. Fetch the target before citing it.
6. **Training memory.** Last resort. Usable only for stable, long-settled facts,
   always flagged as unverified when it matters.

## Routing to context7-expert

When the question is library-specific (API signatures, version behavior, migration),
do not rebuild documentation lookup here. If the `context7-expert` skill is
installed, route through it: it owns the consent gate, mode selection, and budget
rules for Context7 transmission. This skill owns the audit around it (scope,
cross-verification, grading, reporting).

If that skill is not installed on the current harness, fetch it from its canonical
raw URL instead of guessing the lookup workflow:

```text
https://raw.githubusercontent.com/D1ZZY4/agent-skills/refs/heads/main/skills/context7-expert/SKILL.md
```

Reference files follow the same pattern. Replace `SKILL.md` with the reference path,
for example `references/cli-mode.md`.

## Practical rules

- Fetch the page; do not cite a search excerpt. A fetch that fails (bot wall,
  404, redirect) is itself a finding: record it as a fetch failure, not as proof.
- Prefer primary URLs over mirrors and scrapers. If only a mirror loads, say so.
- For documentation sites that reorganize (path migrations), verify the new
  location for at least two or three samples before rewriting every link.
- Never transmit secrets, tokens, personal data, or proprietary code to reach a
  source. Redact queries first or ask.

## Retrieval discipline

- Establish the current date before time-sensitive research so recency claims
  ("latest", "new", "deprecated") anchor to something real.
- Retrieve independent sources in parallel where the harness allows it; batch
  the fetches, then triangulate. Parallel calls share nothing until the
  comparison step, which keeps one source from framing the others.
- Take structured notes per source (claim, quote or locator, source strength)
  as you go. A claim ledger in the report (see `report-format.md`) is built
  from these notes, not reconstructed from memory at the end.
- Deduplicate by origin: three pages quoting the same upstream announcement
  count as one source, not three.
