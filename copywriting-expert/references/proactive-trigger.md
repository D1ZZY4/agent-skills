# Proactive Trigger

When to review, rewrite, or audit copy without being asked, and when to stay quiet.

## When to act

- **A feature adds or changes user-visible language**: buttons, labels, errors, empty states,
  toasts, onboarding steps, tooltips, confirmation dialogs, or any text the user reads or hears.
- **A PR or design doc touches user-facing surfaces**: even when copy is not the primary focus,
  wording drift accumulates, so the right moment to fix it is before it ships.
- **The existing copy reads as generic or blame-oriented**: "Something went wrong", "Invalid
  input", or an "Are you sure?" that never names a consequence are signals to replace, not to
  patch once.
- **A string will be translated**: untranslated or awkwardly translated copy becomes permanent
  in every locale, so check it before marking it final.
- **A confirmation dialog is being added for a routine reversible action**: overuse trains
  users to dismiss dialogs without reading them, which defeats the dialogs that actually matter.
- **A first-run or onboarding flow is being designed**: copy here sets the user's mental model
  of the product, so get it reviewed before it hardens.
- **A destructive or irreversible action needs copy**: naming the specific consequence, affected
  objects, and blast radius is non-negotiable. Do it before the code ships.

## When to stay quiet

- The text is a clearly temporary placeholder that the user has marked as pending review.
- The change is purely structural or backend, with no user-visible string impact.
- The same copy was already reviewed earlier in the conversation, and nothing about the wording,
  audience, or stakes has changed.

## How to offer

Suggest the specific problem and a concrete replacement rather than only flagging the copy.
"This error blames the user; better: `That value doesn't look right`." is more useful than
"consider rewriting this." For high-stakes copy, give the replacement directly. For ambiguous
cases, ask whether the register should be formal or casual before settling on a final version.