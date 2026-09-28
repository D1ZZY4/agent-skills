# Proactive Trigger

This reference decides when the skill becomes relevant. It does not grant permission to transmit a
query.

## Trigger conditions

Auto-load the skill when one or more of these conditions hold:

- the user asks about a named library, framework, SDK, CLI, API, or cloud service
- the user asks about a specific version or migration
- code being written depends on a third-party API whose exact behavior may have changed
- an error clearly originates from a specific external dependency and its documented behavior matters
- the agent is about to state an API signature from memory and cannot establish it from project-local
  evidence
- setup or configuration instructions for a named external technology are requested

The trigger may be inferred from the task. The network lookup may not.

## Stay quiet

Do not invoke Context7 merely because:

- the question is a general language or algorithm concept
- the repository already establishes the answer in authoritative local documentation
- the task is a pure refactor or business-logic discussion
- the user explicitly declined live documentation and nothing material has changed

## Local-evidence gate

Before proposing a remote lookup, inspect the relevant local evidence when available. If a manifest,
lockfile, existing code, or project documentation already resolves the key question, use that evidence
instead of adding network traffic.

Do not confuse "a package is named in the repository" with "its installed version is verified".

## Confirmation is a separate decision

When the trigger fires, present one compact lookup proposal. The proposal must identify:

- library or package
- version strategy
- mode
- final redacted query
- transmission note when project-specific information will leave the local environment

Give a clear default, then wait for explicit confirmation.

Do not ask the user to restate information already present in the task. The proposal exists to let them
approve or change the outbound lookup, not to make them reconstruct the task.

## Repeated lookups

A prior approval does not cover a materially different lookup. A new query, version, library, mode, or
concept requires a new proposal.

A same-parameter repeat caused by a transient transport failure may be retried only when the previous
approval still exactly matches the request and the retry does not alter the transmitted payload.

## Confidence rule

Training knowledge may be used without Context7 when the answer is genuinely independent of a changing
external API. Familiarity with a library is not enough to bypass the trigger when the exact API surface
is uncertain.
