# Library Selection and Query Writing

This reference is shared by MCP and CLI modes. The transport differs; library identity, version fit,
and query quality do not.

## Result fields

Resolved library results may include:

- library ID, usually `/org/project`
- library name and description
- code-snippet coverage
- source reputation
- benchmark or quality score
- available indexed versions

Treat any result field as evidence about the Context7 index, not as proof of package installation or
vendor endorsement.

## Selection process

1. Identify the ecosystem and intended product from the user's task.
2. Exclude candidates that do not match the requested package, scope, or platform.
3. Prefer an exact name match when it is consistent with the ecosystem and task.
4. Prefer official or primary projects over mirrors, forks, and unrelated packages.
5. Prefer an indexed version that matches the confirmed version strategy.
6. Use documentation coverage, source reputation, and benchmark score as supporting signals, not as
   replacements for identity and version fit.
7. If two candidates could materially change the answer, stop and show the candidates before fetching.
8. If no candidate is trustworthy enough, report that and propose a better query instead of guessing.

A high benchmark score never rescues an identity mismatch.

## Version strategy

Use the most relevant strategy explicitly:

- **Project-resolved**: use the version selected by the lockfile when the answer will guide the current
  project.
- **User-specified**: use the concrete version the user named.
- **Latest indexed**: use when the question is specifically about what Context7 currently indexes, or
  when no project version is relevant and the user accepts that distinction.
- **Vendor current release**: do not label this as proven by Context7 alone. Verify the official release
  source when the distinction matters.

If the exact requested version is not indexed, do not silently substitute. Present the closest relevant
indexed version and explain the compatibility limitation before fetching if it could change the answer.

## Confirmation payload

Before the first network request, present:

- exact library name
- version strategy and target version if known
- Context7 library ID if already resolved
- access mode
- final redacted query
- short transmission note when needed

The confirmation applies to that payload. Do not materially rewrite it after confirmation.

## Query writing

Queries should describe one concrete documentation need, not the entire software task.

Prefer:

- a named API or configuration area
- the behavior being verified
- relevant version or feature context when already safe to transmit
- one concept per request

Avoid:

- one-word queries such as `auth` or `hooks`
- broad multi-topic requests when separate focused fetches are practical
- pasting raw logs, source files, or environment dumps
- speculative API names copied from unverified memory

Examples:

| Quality | Example |
| --- | --- |
| Good | `How does JWT authentication configure middleware in Express.js?` |
| Good | `How does React effect cleanup behave with an async subscription?` |
| Bad | `auth` |
| Bad | `hooks` |
| Bad | `routing and auth and caching in Next.js` |

## Sensitive context

Abstract sensitive project details before the confirmation step. Prefer descriptions such as "a private
internal API" over real hostnames or service names when they are not required to identify the library.

If the sensitive detail is necessary to disambiguate the library itself, say so explicitly and let the
user decide whether that exposure is acceptable.
