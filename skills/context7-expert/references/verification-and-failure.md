# Verification and Failure Handling

Use this reference whenever an answer depends on external documentation, network state, tool behavior,
or a version that could have changed.

## Evidence states

Use explicit evidence labels:

- **not checked**: no verification was performed
- **checked and passed**: the requested verification succeeded
- **checked and failed**: the verification ran and failed
- **skipped**: a relevant check existed but was intentionally not run
- **not applicable**: the check does not apply to the current task

Never collapse these into a vague statement such as "verified".

## Context7-backed claim minimum

For claims presented as Context7-backed, verify or retain:

- selected library ID
- indexed version or `latest indexed`
- final query
- access mode
- exact-version versus closest-version status

When timing matters, record the lookup date.

## What Context7 proves

Context7 documentation can establish what the indexed documentation says. It does not automatically
prove:

- the package is installed locally
- the lockfile resolves to that version
- the user's runtime exposes the same behavior
- a generated example compiles in the user's project
- the indexed version is the vendor's newest release

State the distinction whenever it matters to the conclusion.

## Failure classes

Classify failures when possible:

- **transport**: network or connection failure
- **timeout**: request exceeded the available time
- **rate/quota**: service refused because of limits
- **resolution**: no trustworthy library ID found
- **relevance**: result exists but does not answer the requested concept
- **version gap**: requested version is not adequately indexed
- **authentication**: credentials or session state prevented access
- **execution**: local CLI or package-runner command failed

## Retry policy

Retry only when the retry has a concrete purpose.

- A transport retry may reuse the same confirmed payload when the payload is unchanged.
- A relevance retry normally changes the query and therefore requires a new confirmation.
- A different library, version, or mode always requires a new proposal and confirmation.
- Do not repeat identical failures indefinitely.

See `risk-and-budget.md` for the finite operation budget.

## Fallback

When Context7 cannot provide usable evidence:

1. preserve the failure information
2. use project-local evidence when available
3. otherwise use training knowledge only if it is appropriate
4. label the result as not Context7-verified
5. identify what remains uncertain

Do not silently downgrade a documented answer into a memory-based answer.

## Result mismatch

If a response clearly belongs to another library, unrelated topic, or suspicious payload:

- discard it
- do not infer missing details from it
- report the mismatch
- prepare a new lookup only after the required confirmation

## Side-effect verification

If a lookup path performed setup, authentication, package execution, file writes, or other side effects
under explicit authorization, verify the resulting state separately. Do not treat command invocation as
proof that the intended state exists.

## Hard stop

Stop and surface the issue when:

- the query would expose data the user has not approved
- the required library/version cannot be identified reliably
- the remaining evidence gap materially affects the answer and budget is exhausted
- a tool or package runner is unavailable and no approved fallback exists
- verification itself would require an unapproved side effect
