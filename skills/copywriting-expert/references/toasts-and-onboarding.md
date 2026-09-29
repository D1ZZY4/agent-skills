# Toasts and Onboarding

Copy for transient success feedback, undo actions, onboarding, and first-run guidance.

## Toasts and status feedback

- State the completed result plainly: `Project saved` rather than `Success`.
- Offer an action only when the action exists and is relevant, such as `Undo` for a real undo operation.
- Do not put information the user may need later only in a transient toast.
- Use the project's accessible status pattern so the result can be perceived without relying on color or animation.
- Avoid interruptive success feedback for routine operations.
- If the operation only partially completed, say so. Do not report global success when the result is partial.
- Distinguish a request being accepted from the work actually completing. For asynchronous work, use the state the user can know at that moment.

## Undo

Only offer `Undo` when the product actually supports reversing the completed state.

Do not describe an undo as available merely because the previous operation could theoretically be repeated in reverse.

## Onboarding

- Explain immediate value before listing the entire feature set.
- Use real product terminology and current UI examples.
- Ask only for information required for the next step.
- Let users skip or dismiss optional education when the product supports it.
- Keep each step focused on one decision or action.
- State progress for multi-step required flows when users benefit from knowing where they are.
- Avoid promises such as "set up in seconds" unless the product can support the claim consistently.

## Revisitability

When education is optional and important, provide a documented way to discover it again where the product supports that pattern.

## Verification before shipping

Check onboarding copy against the current UI, permission model, feature availability, localization, and actual first-run path. Stale onboarding is worse than concise onboarding because it teaches a false product model.
