# Proactive Trigger

When to reach for Context7 without waiting for the user to name it, and when training data is
enough. The original Context7 rule files described what the skill does but not when to activate
on its own, which is why it kept requiring an explicit "use context7" instead of triggering on
its own.

## When to act

Reach for this skill any time one of these is true, whether or not the user names Context7 or
even names a library explicitly:

- The user asks a setup, configuration, "how do I", or API signature question that names a
  library, framework, SDK, CLI tool, or cloud service, however casually phrased.
- You are about to write, generate, or fix code that calls into a specific library's API, and
  you are not fully certain the method names, signatures, or config shape are still current for
  the library's latest (or user-specified) version.
- The user mentions a specific version of something, for example "Next.js 15", "React 19", or
  "Prisma 6".
- The user pastes an error message or stack trace that clearly originates from a specific
  library, and the fix depends on that library's current behavior rather than general debugging
  logic.
- You catch yourself about to answer from memory about a library's API with a hedge such as
  "I believe" or "as of my training". That hedge is itself the trigger: check the documentation
  instead of stating the hedge.

## Confidence rule

Training-data confidence must be genuinely certain, not just familiar, to skip this skill.
"I've seen this library many times" is not the same as "I am certain this exact API surface is
unchanged in the current version." Default to checking. An unnecessary lookup costs a few
seconds, while a confidently wrong API signature in generated code costs a broken build, or
worse, code that runs but does the wrong thing.

Exceptions where training data alone is fine:

- Timeless language or framework concepts that do not change with library versions, for
  example what a closure is, what REST means, or general algorithmic complexity.
- The user is asking about something with no external library involved at all.
- The task is refactoring, code review, or business logic debugging where no specific library
  API is actually in question, per the "Do not use for" list in SKILL.md.

## How to offer

Activation decides whether documentation is relevant; it does not authorize sending the query.
Relevance and transmission are two separate decisions:

- Present the planned lookup in compact form instead of narrating it. Do not add a separate
  sentence like "I'm going to check Context7 for this" on top of the proposal; weave the lookup
  into the work the way a developer reaches for documentation without narrating the reach.
- The proposal states: the package or library, the version choice (latest, a named version, or
  the project's pinned version), the mode (MCP when available, otherwise CLI), and a one-line
  note when the query carries project-specific detail.
- Wait for the user's answer. Offer a clear default so the user can simply accept it.
- If the user declines or picks a different version, honor that and do not run the query anyway.

This split is the skill's distinguishing behavior: it shows up in context automatically, but it
never transmits anything to Context7 without an explicit user choice.