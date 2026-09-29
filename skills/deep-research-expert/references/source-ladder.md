# Source Authority and Retrieval

No universal source ranking can answer every technical question. Choose authority based on the
claim's subject, then record why the selected source can prove that claim.

## Claim authority matrix

| Claim class | Preferred authority | Useful cross-check |
| --- | --- | --- |
| What this checked-out project uses or pins | Project-local code, lockfile, manifest, CI | Release notes or upstream docs |
| What a vendor documents as supported behavior | Current official documentation | Official repository or release artifact |
| What a release actually ships | Official release artifact, tag, registry, repository | Official changelog or docs |
| Historical behavior or migration | Release notes, tags, diffs, archived official docs | Maintainer issue or announcement |
| Security weakness or incident | Official advisory, CVE record, incident report | Independent technical analysis |
| Benchmark or quantitative comparison | Original benchmark data/methodology | Independent reproduction |
| Academic or scientific claim | Primary study, systematic review, authoritative dataset | Independent replication or synthesis |
| Community experience or known limitation | Maintainer issue, technical discussion | Independent reports and reproduction |
| Market/vendor claim | Vendor documentation for the claim itself | Independent sources for comparative claims |

## Authority rules

- Project-local evidence is strongest for project-local facts. Do not use it as automatic proof of
  vendor-wide behavior.
- Current official documentation is usually strongest for documented current behavior, but it may not
  prove what an installed artifact actually implements.
- A source can be authoritative for one claim and irrelevant to another. Record the claim-source fit.
- Recency does not automatically beat authority. A current secondary article cannot silently override
  a current primary source without explaining the conflict.
- When two strong sources disagree, preserve both, identify the source revisions and dates, and explain
  the claim-specific basis for the conclusion or leave it unresolved.

## Discovery versus evidence

Search results, snippets, summaries, social posts, generated answers, cached previews, and model memory
are discovery aids. They become evidence only after the underlying source has been retrieved and checked.

A URL that was never fetched must not appear in the report as though it was verified. A fetch failure is
recorded as a failure, not converted into proof that the source or feature is absent.

## Independence and deduplication

Count sources by origin, not by number of pages. Three articles reproducing one vendor announcement
are one source origin. An issue linking to the same release note is not an independent confirmation of
the release note's contents.

For important claims, prefer a second source with a genuinely different origin, method, dataset, or
observation. Independence can be impossible for some vendor-specific facts; say so instead of faking
triangulation.

## Provenance record

For every load-bearing source, capture as available:

- canonical URL
- source title
- publisher or repository owner
- source type
- revision, tag, commit, release, or document version
- publication or update date
- retrieval date
- exact locator such as section, heading, line range, or API field
- whether the content was fetched directly or through an intermediate tool
- known limitations or access failures

For GitHub-hosted evidence, prefer immutable commit or tag permalinks when a historical or reproducible
reference matters. Branch URLs can change as the branch advances. GitHub documents commit-based
permalinks as the way to preserve the exact file version being referenced.

## Retrieval discipline

1. Establish the research date when recency matters.
2. Define the claim before choosing the fetch.
3. Fetch the primary source that can prove the claim.
4. Capture the relevant locator and revision.
5. Add independent corroboration when the claim's risk or uncertainty warrants it.
6. Deduplicate shared origins.
7. Record failures and gaps rather than silently substituting a nearby source.

## External lookup and sensitive context

Never place secrets, tokens, personal data, or proprietary code into a remote query merely to make a
search more precise. Prefer public identifiers, URLs, package names, commit IDs, and redacted summaries.
When a local code excerpt is necessary to explain the question, minimize the transmitted content and
obtain authorization when the environment requires it.

## AI-specific provenance

For AI system research, record the model, tool, retrieval context, and evaluation conditions when they
materially affect the result. Provenance is part of the evidence chain, not decorative metadata.
Standards and risk-management frameworks for generative AI treat provenance tracking, and documenting
its limitations, as a useful practice. Cite such a source only after retrieving it, with its locator
and revision, under the same rules as any other load-bearing reference.
