# Verification and Failure Handling

How to distinguish verified copy decisions from reasonable but unverified suggestions.

## Evidence states

Use explicit evidence states when they matter:

- `not checked`
- `checked and passed`
- `checked and failed`
- `skipped`
- `not applicable`
- `partially verified`

Never describe static inspection as if it were runtime verification.

## What to verify

Verify the smallest fact that controls the wording decision.

Examples:

- Does the product really support undo?
- Is this resource actually permanently deleted?
- Does the error state reveal whether a resource exists?
- Is the limit really 10 MB?
- Is this the project's approved term?
- Does the localization framework support the variable structure being proposed?
- Does the current UI expose the status through an accessible mechanism?

Do not test an unrelated subsystem merely to make a copy review look thorough.

## Source preference

Prefer:

1. actual product behavior
2. current project documentation and tests
3. approved product terminology
4. authoritative external language or domain sources
5. general references

When two sources disagree, identify the conflict and prefer the source with authority for the specific claim.

## High-stakes copy

For legal, security, privacy, safety, account deletion, billing, permissions, or similarly consequential copy, verify every material claim you are about to put in the user's mouth.

Do not convert a product possibility into a guarantee. `May`, `can`, and `will` are materially different claims.

## Accessibility verification

Separate these questions:

- Is the copy understandable and appropriately labeled?
- Is the UI actually exposing that copy with the expected semantics?
- Has the result been tested with supported assistive technologies?

A content-only review can answer the first and flag the other two. It cannot honestly certify the implementation without evidence.

## Localization verification

Distinguish:

- source-language correctness
- translation correctness
- rendering correctness
- locale-aware formatting correctness

A sentence can be linguistically correct and still fail because variables, pluralization, or layout are implemented incorrectly.

## Failure handling

If verification is unavailable:

- continue with safe project-local evidence when possible
- mark the uncertain decision explicitly
- do not invent a citation, test result, product capability, or translation validation
- for high-stakes copy, do not present the wording as fully verified

If a check fails, report the failing fact and adjust the copy or stop. Do not hide a failed verification behind polished prose.
