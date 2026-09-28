# Risk and Operation Budget

Use a finite budget for Context7 documentation operations. The goal is not to maximize calls; it is to
obtain enough evidence to answer reliably while limiting network exposure and repeated tool use.

## What counts

Count each outbound documentation operation:

- library resolution
- documentation fetch
- relevance retry
- alternate candidate check
- alternate mode or source check when it changes the remote request

User confirmation, local file inspection, and local reasoning do not consume the Context7 lookup budget.
Setup, authentication, and skills-management mutations are separate operations with their own explicit
approval. Do not use this budget to justify them.

## Risk tiers

### Low risk

Examples:

- one library and one stable API concept
- one clearly pinned version
- a lookup expected to resolve and fetch once

Budget: up to 3 outbound operations.

Typical path:

1. resolve, unless exact ID is supplied
2. fetch
3. one focused retry only if justified

### Medium risk

Examples:

- version-sensitive framework configuration
- library-specific errors
- closely related concepts whose interaction matters
- migration guidance that affects code structure

Budget: up to 5 outbound operations when each extra call has a stated purpose.

### High risk

Examples:

- security-sensitive configuration
- authentication or authorization
- production deployment or infrastructure behavior
- breaking migrations
- database schema or data migration guidance
- payments or other high-impact integrations
- multi-library compatibility decisions

Budget: up to 7 outbound operations when necessary. Prefer exact-version and official sources.

## Retry rules

A retry is justified only when the previous result was plausibly a relevance failure, not merely because
the desired answer was inconvenient.

- Do not repeat the identical failed query more than once.
- A changed query is a new outbound payload and requires a new confirmation.
- A different library, version, or mode requires a new proposal and confirmation.
- Do not increase the budget merely because the first query was poorly written.

## Stop conditions

Stop when:

- the requested evidence is established sufficiently
- the remaining uncertainty is not worth another call
- the budget is exhausted
- the service is unavailable
- the available indexed version cannot support the requested claim

Report what was verified and what remains unresolved.

## Budget and security

A larger budget never overrides:

- user consent for network transmission
- query redaction
- npx execution approval
- setup or authentication approval
- prompt-injection boundaries

Do not use the budget as a reason to keep probing after the user has declined further lookup.
