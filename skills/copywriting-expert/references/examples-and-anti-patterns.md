# Examples and Anti-Patterns

Use these as review patterns, not as universal strings. Project terminology, behavior, locale, and accessibility requirements take precedence.

## Buttons

| Weak | Better | Why |
| --- | --- | --- |
| `OK` | `Delete project` | Names the action |
| `Submit` | `Send invite` | Names the result |
| `Yes / No` | `Delete / Cancel` | Removes ambiguity |

## Errors

| Weak | Better | Why |
| --- | --- | --- |
| `Something went wrong` | `We couldn't save your changes. Try again.` | States impact and real recovery path |
| `Invalid input` | `Enter a valid repository name.` | Identifies the correction |
| `Error 403` | `You don't have permission to edit this project.` | Translates the relevant state |

## Empty states

| Weak | Better | Why |
| --- | --- | --- |
| `No items yet` | `Create your first project` | Orients and acts |
| `No results` | `No projects match these filters.` | Preserves the distinction between filtering and absence |
| blank | `You've archived all your tasks.` | Explains the current state |

## Confirmations

```text
Delete this project?
This permanently deletes "Q3 Roadmap" and its 12 files. You cannot undo this.

Delete project / Cancel
```

Only use the specific name and count when the product actually knows and may display them.

## Toasts

| Weak | Better | Why |
| --- | --- | --- |
| `Success` | `Project saved` | States the result |
| `Your changes have been successfully saved` | `Saved` | Removes filler |
| `Saved` | `Saved. Undo` | Adds a real action only when undo exists |

## Onboarding

```text
Create your first report
See live metrics from your connected data.
```

The value claim must match the actual product behavior.

## CLI

Weak:

```text
ERROR: failed to process request
```

Better:

```text
Couldn't load reports.
Check your connection and try again.
```

For machine-readable output, do not replace a stable schema with prose.

## Accessibility and localization anti-patterns

- visible label says `Delete`, accessible name says `Remove this thing` without a reason
- `1 item(s)` instead of locale-aware pluralization
- sentence fragments concatenated in English order
- essential status conveyed only by a toast that is not exposed to assistive technology
- translated strings that preserve a source-language pun but lose the intended meaning

## Scope anti-patterns

- turning a one-string fix into a product-wide rewrite
- changing an established product term because a synonym looks nicer
- changing a copy string that is also a parser, test fixture, analytics key, or API value without inspecting its references
- reviewing unrelated screens merely because they use similar copy

## Claim anti-patterns

- "Never lose your work" when recovery is not guaranteed
- "Secure" or "private" without a documented basis
- "Instant" or "real-time" when latency varies materially
- exact limits, time windows, or availability without evidence

## Full review example

Before:

```text
Title: Confirm
Body: Are you sure you want to do this? This action is permanent and cannot be undone.
Buttons: Yes / No
```

After:

```text
Title: Delete this project?
Body: This permanently deletes "Q3 Roadmap" and its 12 files. You cannot undo this.
Buttons: Delete project / Cancel
```

The improvement works because it names the operation, the target, the consequence, and the actual confirm action. It does not add claims beyond the known behavior.
