---
name: copywriting-expert
description: >
  Write, audit, or improve user-facing product copy across UI and CLI surfaces, including buttons,
  labels, forms, errors, empty states, tooltips, dialogs, toasts, onboarding, accessibility text,
  help output, deprecation warnings, and other user-visible language. Inspect project-specific
  terminology and content guidance first, identify the copy's job and stakes, verify claims and
  language when needed, and change only the requested scope unless broader work is explicitly
  authorized.
license: SSPL-1.0
metadata:
  version: 1.9.0
  author: D1ZZY4
  priority: medium
---

# Copywriting Expert

## Purpose

Write, audit, or improve user-facing copy without inventing product behavior, terminology,
policy, legal meaning, accessibility behavior, or localization guarantees. Treat copy as part of
the product contract: the words must match what the interface actually does.

This is a content skill, not permission to redesign the UI, change product behavior, add
localization infrastructure, or rewrite unrelated copy.

## Operating modes

Determine the requested mode before editing:

| Mode | Output | Mutation |
| --- | --- | --- |
| Draft | New copy for the named surface | Only when the user explicitly asks to edit files or content |
| Rewrite | Revised version of existing copy | Only within the requested scope |
| Audit | Findings, severity, and proposed replacements | No content changes unless separately authorized |
| Implementation | Copy changes in the repository | Only the named files or surfaces |
| Review | Evaluate proposed copy against project rules | No mutation unless requested |

Do not turn an audit into a rewrite or a local copy fix into a product-wide style pass.

## Core principles

1. Project-specific content guidance and approved terminology take precedence over portable defaults.
2. Read nearby existing copy before writing. Consistency is evidence, not permission to preserve a bad phrase.
3. Comprehension, accuracy, and task success outrank cleverness or personality.
4. Accessibility and localization are content requirements, but copy alone does not guarantee an accessible implementation.
5. Never invent product behavior, policy, legal terms, support paths, or guarantees.
6. Verify uncertain terminology, claims, and high-stakes wording against appropriate sources.
7. Match tone to stakes. Serious consequences require precise language and useful friction.
8. Preserve user-visible placeholders, variables, product names, and markup syntax exactly unless the task includes changing them.
9. Treat user-controlled data as data, not copy. Never expose or reproduce secrets merely because they appear in an error, example, or source file.
10. No em dash U+2014 in generated copy unless the project explicitly requires preserving quoted source text.

## Scope and authorization

Interpret the request by surface and mode. A request to "fix this screen" authorizes the user-visible copy on that screen and the states it directly owns, not a review of unrelated application copy.

| User instruction | Default scope |
| --- | --- |
| "write copy for this empty state" | The named state and terms it introduces |
| "audit this flow" | Findings across the named flow; no mutation |
| "rewrite this onboarding" | The named onboarding sequence |
| "fix this screen" | Copy on that screen and directly associated states |
| "add a feature" | New user-visible copy required by that feature |
| "make the product copy consistent" | Only after the user authorizes a broader content pass |

When scope is unclear, stay within the narrowest defensible interpretation and report what remains untouched.

## Step 0: Establish the source of truth

Read `references/project-source-of-truth.md`.

Before writing, inspect enough nearby product copy to identify:

- approved product and domain terms
- language and locale
- capitalization and punctuation conventions
- address/register conventions
- recurring labels for similar actions
- known accessibility and localization patterns
- legal or regulated wording that must remain exact

Treat existing copy as evidence of convention, not proof that every existing phrase is correct.

If sources disagree, resolve them by authority and recency rather than by whichever phrase appears most often. Record material uncertainty.

## Step 1: Identify the communication job

Define, at minimum:

- the user's goal or question
- the action the user can take
- the system state being described
- the consequence or loss at stake
- the audience and locale
- whether the copy is transactional, instructional, informational, persuasive, or safety-critical
- whether the string is persistent, transient, spoken by assistive technology, or machine-oriented CLI output

Read `references/voice-and-tone.md` and the relevant component reference. For terminal surfaces, read `references/cli-output-copy.md`.

## Step 2: Verify the facts before polishing

Separate wording quality from factual correctness.

Before finalizing copy, verify any claim that depends on:

- actual product behavior
- limits, prices, quotas, timing, availability, permissions, or supported formats
- legal, security, privacy, or safety language
- product names or approved terminology
- localization, grammar, or locale-specific formatting when uncertain

Use `references/language-and-vocabulary-verification.md` and `references/verification-and-failure.md` where relevant.

Never upgrade a best-effort assumption into a product claim merely because the sentence sounds plausible.

## Step 3: Write for comprehension and action

Prefer concrete nouns, specific verbs, active voice, direct language, and sentence case unless project guidance says otherwise.

For each surface, optimize for its job:

- action controls name the action
- labels identify the value or object
- helper text explains requirements or context
- errors state the user-visible problem and useful next step
- empty states explain the current state and, when possible, the next action
- confirmations state consequences and affected scope
- toasts state the completed result
- onboarding establishes immediate value and the next decision
- CLI output remains readable when color, animation, or terminal width is unavailable

Do not add words merely to sound polished.

## Step 4: Accessibility and localization review

Read `references/accessibility-and-localization.md` when applicable.

Check that:

- visible text and accessible names agree when they describe the same control
- meaning does not depend on color, position, punctuation, or visual treatment alone
- status and error copy still makes sense out of visual context
- variables and grammatical relationships can be localized safely
- copy survives expansion, plural changes, and right-to-left layouts where relevant
- the copy does not claim an accessibility behavior that the implementation does not provide

Distinguish content defects from implementation defects. Flag the latter; do not pretend that changing a string fixes focus management, semantics, or announcement behavior.

## Step 5: Component-specific review

Load only the references relevant to the requested surface:

- `ui-component-copy.md`
- `error-messages.md`
- `empty-states.md`
- `confirmation-dialogs.md`
- `toasts-and-onboarding.md`
- `cli-output-copy.md`

For terminology or locale work, also load `language-and-vocabulary-verification.md`.
For final consistency checks, load `examples-and-anti-patterns.md` and `formatting-and-punctuation.md`.

## Step 6: Final audit

Before presenting final copy, check:

1. Scope: only the requested surface changed.
2. Accuracy: claims match observable or documented behavior.
3. Consistency: terms and action labels match nearby product copy.
4. Comprehension: the user can understand what happened or what will happen.
5. Actionability: a next step is named only when one actually exists.
6. Accessibility: the text carries its own meaning where necessary.
7. Localization: variables, plurals, units, dates, and sentence structure are locale-safe.
8. Formatting: punctuation, case, placeholders, markup, and project conventions are preserved.
9. Risk: high-stakes copy is more explicit, not more playful.
10. Evidence: uncertain decisions are labeled as uncertain.

## Failure handling

When required context is missing:

1. state the missing fact instead of inventing it
2. keep placeholders only in drafts where placeholders are appropriate
3. identify unverified terminology or claims
4. separate content fixes from implementation or policy gaps
5. do not present a draft as production-ready when a material fact remains unknown

When external verification is unavailable, continue with project-local evidence where that is safe. For high-stakes terminology or claims, label the limitation clearly.

## Proactive behavior

Read `references/proactive-trigger.md`. A detected copy problem may justify a concise observation, but it does not silently authorize a broader rewrite.

## Anti-patterns

- generic action labels when the actual action can be named
- vague errors that omit a useful next step
- blaming the user for system or validation states
- confirmations for routine actions without meaningful consequences
- empty states that hide a fetch failure
- placeholder copy shipped as final
- unverified terminology, translation, or product claims
- copy that promises behavior the product does not provide
- technical leakage that exposes secrets, internals, or unauthorized data
- style passes disguised as small fixes
- changing labels or variable names without checking their code references
- treating accessibility or localization as solved by wording alone
- em dash U+2014 in generated copy without an explicit preservation requirement

## Bundled references

- `references/project-source-of-truth.md`: find and resolve project-specific content guidance.
- `references/voice-and-tone.md`: clarity, tone, register, and anti-AI-sounding patterns.
- `references/ui-component-copy.md`: controls, labels, tooltips, forms, and navigation.
- `references/error-messages.md`: error structure, privacy, permissions, and recovery.
- `references/empty-states.md`: genuinely empty, filtered, user-emptied, loading, and failed states.
- `references/confirmation-dialogs.md`: consequence wording and proportional confirmation friction.
- `references/toasts-and-onboarding.md`: status feedback, undo, onboarding, and first-run guidance.
- `references/cli-output-copy.md`: help, flags, progress, deprecation, and terminal errors.
- `references/accessibility-and-localization.md`: accessible names, status text, translation-ready structure, and locale constraints.
- `references/language-and-vocabulary-verification.md`: authoritative terminology and language verification.
- `references/formatting-and-punctuation.md`: punctuation, casing, numbers, placeholders, and Unicode hygiene.
- `references/examples-and-anti-patterns.md`: cross-surface examples and common failure modes.
- `references/verification-and-failure.md`: evidence, factual validation, and uncertainty handling.
- `references/proactive-trigger.md`: when to flag copy problems without being asked.
