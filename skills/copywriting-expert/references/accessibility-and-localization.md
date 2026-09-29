# Accessibility and Localization

Copy requirements for accessible names, status and error messages, labels, alternative text, and localization-ready message structure. Content guidance does not replace implementation or assistive-technology testing.

## Accessible names and visible labels

- Give each interactive control a meaningful accessible name when its visible content is insufficient.
- Prefer visible text as the accessible name when possible. This reduces divergence between what sighted users see and what assistive-technology users hear.
- Keep the visible label and programmatic name aligned. Where WCAG 2.5.3 applies, the accessible name should contain the visible label text.
- Use `aria-label` only when there is no suitable visible naming source or when the project has a documented reason to use it. Do not overwrite useful visible content casually.
- Do not rely on icons, color, position, capitalization, or punctuation alone to communicate the purpose or state of a control.
- Flag missing accessible-name or semantic behavior as an implementation issue when copy alone cannot fix it.

W3C guidance describes accessible names as a core part of usable assistive-technology semantics and recommends preferring visible text as the naming source when possible. See the sources below.

## Forms and validation

- Use a visible field label for the field's identity. Put format requirements and examples in helper text or other persistent context.
- Associate validation copy with the affected field and provide a summary when multiple fields need attention.
- Do not encode error state only with color or iconography.
- Validation text should identify the value that needs attention and the correction when the correction is knowable.
- Avoid rewriting technical field names into user-visible labels unless the product already uses that terminology.

## Status and asynchronous updates

- Status text should remain understandable when encountered without the surrounding visual context.
- State the meaningful result, not merely that an internal event occurred.
- Use the project's status/live-region pattern for announcements. Copy cannot guarantee that assistive technology will announce a string unless the implementation exposes it correctly.
- Do not put critical information only in a transient toast or animation.
- When a state persists, the durable UI should also expose the result where appropriate.

## Links and navigation

- Link text should identify the destination or action. Avoid standalone "click here" or "learn more" labels when the surrounding structure does not provide enough context.
- Keep visible link text and its accessible name aligned when they refer to the same destination.
- Do not use a tooltip or visually hidden text to compensate for a fundamentally ambiguous visible control when the label can be improved directly.

## Images and non-text content

- Informative images need alternative text that conveys their relevant meaning or purpose.
- Decorative images should not introduce redundant spoken content.
- If an icon communicates a state that the adjacent text does not state, ensure an accessible text alternative exists.

## Localization-ready copy

- Do not assemble sentences by concatenating fragments whose order depends on English grammar.
- Keep variables explicit and documented, for example `{count}` and `{projectName}`.
- Give translators enough context to know what a variable means and whether it is a noun, number, date, or user-provided string.
- Use the project's message-formatting and pluralization framework. Do not hand-roll singular/plural logic in copy strings.
- Expect plural, gender, politeness, agreement, and word order to vary by language. Not every language maps cleanly to English categories.
- Keep room for text expansion and avoid designs that assume the source string length.
- Use locale-aware formatting for dates, times, numbers, currencies, and units.
- Check right-to-left rendering when the locale requires it.
- Avoid idioms, jokes, or unexplained abbreviations in strings intended for broad localization unless the project explicitly accepts them.

Unicode CLDR documents language-specific plural categories and is a useful implementation reference for locale-aware plural handling. See the sources below.

## Final check

For high-impact surfaces, review both the copy and the rendered behavior. A good string with a broken accessible name, missing status announcement, clipped translation, or incorrect plural rule is still a product defect.

## Sources

- W3C WAI-ARIA APG, Providing Accessible Names and Descriptions: https://www.w3.org/WAI/ARIA/apg/practices/names-and-descriptions/
- W3C WCAG, Label in Name: https://www.w3.org/WAI/WCAG21/Understanding/label-in-name
- Unicode CLDR, Plural Rules: https://cldr.unicode.org/index/cldr-spec/plural-rules
