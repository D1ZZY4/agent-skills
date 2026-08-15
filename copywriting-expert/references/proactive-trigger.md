# Proactive Trigger Conditions

When to review, rewrite, or audit copy without being asked, and when to stay quiet.

## Review or rewrite copy without being asked when

- **A feature adds or changes user-visible language**: buttons, labels, errors, empty states,
  toasts, onboarding steps, tooltips, confirmation dialogs, or any text the user reads or hears.
- **A PR or design doc touches user-facing surfaces**: even if copy is not the primary focus,
  wording drift accumulates and the right moment to fix it is before it ships.
- **The existing copy reads as generic or blame-oriented**: "Something went wrong", "Invalid
  input", "Are you sure?" without consequence, these are signals to replace rather than explain
  once.
- **A string will be translated**: untranslated or awkwardly translated copy becomes permanent in
  every locale. Check it before marking it final.
- **A confirmation dialog is being added for a routine reversible action**: overuse trains users
  to dismiss dialogs without reading, which defeats the ones that actually matter.
- **A first-run or onboarding flow is being designed**: copy here sets the user's mental model
  of the product, get it reviewed before it hardens.
- **A destructive or irreversible action needs copy**: naming the specific consequence, affected
  objects, and blast radius is non-negotiable, do it before the code ships.

## When not to bother

- The text is a clearly temporary placeholder that the user has marked as pending review.
- The change is purely structural or backend with no user-visible string impact.
- The same copy was already reviewed earlier in the conversation and nothing about the wording,
  audience, or stakes has changed.

## Offer, don't just declare

When copy needs attention, suggest the specific problem and a concrete replacement rather than
only flagging it. "This error blames the user; better: `That value doesn't look right`" is more
useful than "consider rewriting this." For high-stakes copy, give the replacement directly; for
ambiguous cases, ask whether the register should be formal or casual before settling on a final
version.
