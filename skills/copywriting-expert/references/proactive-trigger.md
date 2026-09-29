# Proactive Trigger

When to flag or improve copy without an explicit copywriting request, and when to leave it alone.

## Trigger conditions

Raise a concise copy concern when:

- new or changed code introduces user-visible language with a concrete comprehension, accuracy, accessibility, localization, privacy, or consistency problem
- a destructive or high-impact action lacks consequence-aware copy
- an error message hides the actual user-visible failure or offers a recovery path that does not exist
- a fetch failure is presented as an empty state
- an important translation or product term is uncertain
- a new confirmation dialog adds friction to a low-risk reversible action without a clear reason
- onboarding claims value or capability that the product does not actually provide

Do not trigger merely because the copy could be phrased differently.

## What proactive review authorizes

A proactive finding authorizes an observation or a proposed replacement in the response. It does not authorize editing unrelated files or performing a product-wide voice pass.

When the user is already editing a named surface, a small copy correction within that surface can be included when it is clearly part of the requested change. Broader cleanup requires broader authorization.

## Stay quiet when

- the copy is intentionally temporary and clearly marked for review
- the change is non-user-visible
- the string was already reviewed and no material fact, audience, locale, or stakes changed
- the user asked for a draft and only a preference difference exists
- an existing style choice is unfamiliar but documented or consistently used

## Confidence rule

Distinguish defects from preferences.

- Defect: objectively misleading, inconsistent with verified behavior, inaccessible in a material way, unsafe to localize, or clearly outside project rules.
- Preference: one of multiple reasonable phrasings that fit the product.
- Uncertainty: not enough evidence to classify it.

Present these categories differently. Do not label a subjective tone preference as an error.

## How to report

Lead with the concrete problem and the smallest useful replacement:

```text
This error blames the user.
Better: `That value doesn't look right.`
```

For uncertain claims, state the missing evidence instead of fabricating certainty.
