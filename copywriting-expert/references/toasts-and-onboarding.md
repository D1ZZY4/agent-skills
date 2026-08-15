---
name: Toasts and Onboarding
description: Guidance for transient success feedback, undo actions, and first-run education.
---

# Toasts and Onboarding

Toast and success-feedback copy, plus onboarding and first-run guidance. Toasts state the
completed result plainly and include undo actions only when relevant. Onboarding explains immediate
value, asks for information only when needed, and keeps each step focused.

## Toasts and success feedback

- State the completed result plainly: "Project saved", not "Success".
- Include the next useful action only when it is genuinely relevant, such as an `Undo` action
  for a reversible change.
- Do not put essential information only in a transient toast. Keep durable status in the page or
  control when the user may need it later.
- Use an assertive status pattern that the project's accessibility system exposes to assistive
  technology. Do not rely on color or animation alone.
- Avoid interrupting the user for routine success messages. Reserve prominent alerts for failures,
  consequences, or actions that require attention.

## Onboarding and first-run guidance

- Explain the immediate value and the next action before listing every available feature.
- Use the product's real terminology and examples, not placeholder tours that become stale.
- Let users skip or dismiss non-essential education, and provide a way to revisit it later when
  the product supports that pattern.
- Ask for information only when it is needed for the next step. Defer optional setup.
- Keep each step focused on one decision or action, and state progress when the flow has multiple
  required steps.
- Verify that onboarding copy still matches the current UI, localization rules, and permission
  model before shipping.