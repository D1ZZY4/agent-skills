# Confirmation and Destructive-Action Dialogs

Copy for consequential actions. The goal is informed confirmation, not ritual friction.

## Confirm only when confirmation adds information

Do not show a confirmation dialog merely because an operation exists. Prefer a direct action plus undo when an action is low-risk and easily reversible.

A confirmation is justified when the user benefits from a clear pause before a meaningful consequence.

## State the consequence

Name:

- the object affected
- the action that will occur
- whether it can be undone
- any important secondary effects
- who else loses access or data, when relevant

Weak:

```text
Are you sure?
```

Better:

```text
Delete this project?
This permanently deletes the project and its files. You cannot undo this.
```

Do not invent permanence. Verify reversibility from the actual product behavior.

## Name the confirm action

Prefer:

```text
Delete project / Cancel
```

over:

```text
OK / Cancel
```

The destructive control should make the consequence recognizable without requiring the user to reread the entire dialog.

## Scale friction to risk

Use progressively stronger friction for actions that are more consequential, less reversible, or have a larger blast radius.

| Risk | Copy treatment |
| --- | --- |
| Low-risk and easily reversible | Usually no blocking confirmation; prefer undo |
| Reversible but surprising | State how and when it can be restored |
| Irreversible but narrow | State exactly what is lost |
| Irreversible or high-impact | State full scope and important secondary effects; consider explicit confirmation input if the product uses that pattern |

Do not assume a typed-name confirmation is appropriate just because an action is destructive. Match the pattern to the product's existing security and interaction model.

## Blast radius

When more than the named object is affected, say so:

```text
Remove this member?
They will lose access to all projects in this workspace.
```

Do not use a person's name, count, or resource detail unless the product actually knows it and is allowed to expose it.

## Button order and escape behavior

Copy should remain understandable regardless of platform-specific button placement. Do not encode meaning only as "left button" or "right button" guidance.

If keyboard dismissal or escape can trigger an action, verify the implementation before writing copy that assumes a particular cancellation behavior.
