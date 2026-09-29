# Error Messages

Copy that accurately describes a user-visible failure without blaming the user, leaking sensitive information, or pretending a recovery path exists.

## Core structure

When information is available and useful, use this order:

1. What happened?
2. Why did it happen?
3. What can the user do next?

Example:

```text
We couldn't save your changes.
Your connection was interrupted. Try again.
```

Do not force all three parts into every message. A reason or next step that is unknown or unavailable should be omitted rather than invented.

## Describe the user-visible state

Translate internal failures into the language of the task:

```text
We couldn't save your changes.
```

not:

```text
PUT /api/v2/documents returned 503.
```

Technical details can be secondary diagnostics when they help support or debugging and are safe to expose.

## Avoid blame and false certainty

Prefer neutral framing:

```text
That email address doesn't look right.
```

over:

```text
You entered an invalid email.
```

For system failures, do not imply the user caused the problem.

Do not say "try again" when retrying cannot resolve the underlying state.

## Match severity

Use strong terms only when the user-facing consequence warrants them. A missing required field is not a "critical error".

High-severity copy should be calm and exact. Do not soften a serious consequence with jokes or casual phrasing.

## Recovery paths

Classify the failure before offering an action:

- recoverable now: retry, correct, reconnect, or undo
- recoverable elsewhere: request access, contact an administrator, restore a resource
- not actionable by the user: acknowledge the failure and point to status/support information when appropriate

Never invent a support channel, status page, recovery action, or expected recovery time.

## Permission and privacy

Authorization failures require special care. Tell legitimate users what they can safely do without revealing protected resource existence, another user's data, internal paths, secrets, tokens, or authorization details.

Distinguish known states such as "you do not have access" from "this resource no longer exists" only when the product is allowed to make that distinction to the current user.

## Dynamic values

Do not echo arbitrary user-controlled values into errors without considering privacy, escaping, and whether the value is appropriate to expose.

Use locale-aware formatting for counts, dates, sizes, and currencies. Preserve stable diagnostic identifiers only where the project supports them.

## Examples

| Situation | Weak | Better |
| --- | --- | --- |
| Required field | `Error: field required` | `Enter your project name` |
| Wrong password | `Invalid credentials` | `That password doesn't match. Try again or reset it.` |
| Network failure | `Something went wrong` | `We couldn't connect. Check your internet and try again.` |
| File too large | `Upload failed` | `This file is too large. The maximum is 10 MB.` |
| No permission | `Access denied` | `You don't have permission to view this project. Ask an admin for access.` |
| Unknown server failure | `Error 500` | `We couldn't load your projects. Try again shortly.` |
