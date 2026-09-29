# UI Component Copy

Copy rules for controls, labels, tooltips, forms, navigation, and other common interface surfaces.

## Buttons and actions

- Lead with the actual action: `Save changes`, `Delete project`, `Send invite`.
- Keep labels concise, generally 1 to 3 words when the action remains unambiguous.
- Move explanatory context into surrounding copy when the button would otherwise become a sentence.
- Avoid generic `OK`, `Submit`, or `Yes` when the action can be named.
- In a pair, make the consequences of the primary and secondary actions easy to distinguish.
- Do not use the same label for materially different actions in the same flow unless the project has a deliberate navigation convention.

## Labels

- Name the field or concept, not the instruction: `Email` rather than `Enter your email`.
- Keep required/optional marking consistent across the same form.
- Avoid internal abbreviations unless they are genuinely understood by the intended audience.
- Preserve established product terms even when a synonym seems more natural.

## Placeholders

Use placeholders for examples or format hints, not essential instructions.

```text
Label: Repository URL
Placeholder: https://github.com/org/repo
```

Placeholders disappear when the user types. Anything they need while editing belongs in a label or persistent helper text.

## Helper text

Use helper text for persistent constraints, audience context, or format requirements:

```text
Visible to everyone with access to this workspace.
```

Avoid repeating the label without adding information.

## Validation

State the actual issue and the correction when it is knowable:

```text
Repository name must contain only letters, numbers, and hyphens.
```

Do not rely on red text or a green border alone to communicate state.

## Tooltips

- Add information that is not already obvious from the control.
- Keep tooltips short, generally one sentence.
- Do not hide essential consequences or instructions behind hover-only UI.
- Ensure tooltip language does not become the only accessible description of a control when the control needs a persistent name.

## Navigation

- Use nouns for destinations and verbs for actions, consistently within the same control group.
- Keep tabs or filters structurally parallel.
- Name breadcrumbs as the path through the product, not as implementation actions.
- Do not use `Recommended` as decorative praise. Use it only when the product has a documented basis for the recommendation.

## Copy and implementation contracts

Before renaming a string, check whether it is also used as:

- an analytics identifier
- a localization key
- a test fixture
- a parser input
- a keyboard shortcut label
- an accessibility name
- a URL or command value

Do not assume a user-visible string is presentation-only.
