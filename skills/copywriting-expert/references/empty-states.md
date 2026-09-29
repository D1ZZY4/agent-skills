# Empty States

How to distinguish genuine absence from filters, user actions, loading, and failures, then write the minimum useful orientation and next step.

## First determine the state

An empty presentation is not automatically an empty state. Identify the state machine first:

| State | Meaning | Copy direction |
| --- | --- | --- |
| New | Nothing has been created yet | Explain what belongs here and how to create it |
| Filtered | Existing content is hidden by search or filters | State that no items match and offer a way back |
| User-emptied | The user archived or deleted content | Acknowledge what happened and explain recovery when available |
| Permission-limited | Content exists but is not visible to the user | Use access-denied copy, not "nothing here" |
| Loading | Data has not arrived yet | Describe the loading state, not absence |
| Failed | The fetch or operation failed | Use error copy |

Never hide a fetch failure behind a generic empty message.

## What a genuine empty state should answer

1. What belongs in this space?
2. Why is it empty now?
3. What can the user do next, if anything?

The third point is optional. Do not invent an action when the user cannot change the state.

## Action labels

Use a button or link that names the actual action:

```text
Create your first project
```

is stronger than:

```text
Get started
```

when project terminology and behavior support the specific label.

## Filtered empty

Say that the current query or filters produced zero results:

```text
No projects match these filters.
Clear filters
```

Do not imply that the workspace contains no projects when the product only knows that the current query returned none.

## User-emptied state

Reflect the known action:

```text
You've archived all your tasks.
View archived tasks
```

Only mention recovery or archive behavior when the product actually provides it.

## Loading and transitions

- Use loading copy only when it adds value beyond the loading indicator.
- Say what is loading, not that the content is empty.
- If loading fails, switch to the correct error state.
- Do not let stale empty-state copy remain visible while fresh data is still being resolved.

## Personality

Personality may be useful in low-stakes empty states, but it must not replace orientation, state explanation, or the next useful action.
