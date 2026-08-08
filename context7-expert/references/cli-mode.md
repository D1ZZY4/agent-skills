# CLI Mode

Full detail for when no Context7 MCP server is connected but a shell/bash tool is available.
Prefer an already-installed `ctx7` CLI. A transient `npx` invocation is a fallback only when
network access and package execution are permitted for the current request. If that permission
has not already been given, ask before using the network-backed fallback.

## Running commands

Before choosing a command, probe the local CLI without changing the project:

```bash
command -v ctx7
ctx7 --version
```

If the executable is missing or the version check fails, treat the CLI as unavailable. Use the
transient `npx` fallback only when network-backed package execution is already approved, and
record that fallback was used.

If `ctx7` is installed, use it directly:

```bash
ctx7 library <name> "<query>"
ctx7 docs <libraryId> "<query>"
```

If it is not installed and network-backed package execution has been approved, use the fallback:

```bash
npx ctx7@latest library <name> "<query>"
npx ctx7@latest docs <libraryId> "<query>"
```

Do not install the CLI globally as part of a normal documentation lookup. Record or report the
CLI version when reproducibility matters.

## Step 1: Resolve a library

```bash
npx ctx7@latest library "Next.js" "How to set up app router with middleware"
```

You MUST run this first to get a valid library ID, UNLESS the user already gave one directly in
`/org/project` or `/org/project/version` format.

- Use the library's proper official name and punctuation ("Next.js" not "nextjs",
  "Customer.io" not "customerio", "Three.js" not "threejs"). If results look wrong, try an
  alternate spelling before rewriting the whole query.
- Always pass a query argument, it's required and directly affects ranking.
- Do not include sensitive or confidential information (API keys, passwords, credentials,
  personal data, proprietary code) in the query.

For the selection criteria once results come back, see `selection-and-query-writing.md`.

Library IDs require a leading `/`, for example `/facebook/react`, not `facebook/react`.

### Version-specific IDs

```bash
# General (latest indexed)
npx ctx7@latest docs /vercel/next.js "How to set up app router"

# Version-specific
npx ctx7@latest docs /vercel/next.js/v14.3.0-canary.87 "How to set up app router"
```

The available versions are listed in the `library` command's output. Prefer an exact match. If
none exists, use the closest match only when it is relevant, and explicitly report that the
indexed version was a closest match rather than the exact version requested.

## Step 2: Query documentation

```bash
npx ctx7@latest docs /facebook/react "How to clean up useEffect with async operations"
```

See `selection-and-query-writing.md` for query-writing rules, they apply the same way here as
in MCP mode.

The output contains two kinds of content: code snippets (titled, language-tagged blocks) and
info snippets (prose explanations with breadcrumb context).

Useful optional flags for scripting or filtering large output. Do not assume `jq` or `grep` is
available, and do not fail the documentation lookup merely because an optional filter is not:

```bash
npx ctx7@latest library react "How to use hooks for state management" --json | jq '.[0].id'
npx ctx7@latest docs /facebook/react "How to use hooks" --json
npx ctx7@latest docs /vercel/next.js "middleware for route protection" | grep -A5 "middleware"
```

## Call budget

Read `risk-and-budget.md` for the operation budget. Three operations is the default. A
documented increase to five or seven is allowed only for medium- or high-risk questions, when
each additional operation has a clear purpose. Count every `library` resolution, `docs` fetch,
and retry toward the same finite budget.

## Authentication

Works without authentication. Do not initiate login, logout, or credential changes during a
normal documentation lookup. If the user explicitly requests authentication, explain what will
change and use the workspace's approved secret or integration flow. Never ask the user to paste
an API key into chat, a shell command, a query, or a committed file.

## Error handling

If a command fails with a quota error ("Monthly quota reached" or "quota exceeded"):

1. Tell the user their Context7 quota is exhausted, plainly.
2. Mention authentication as an optional user-controlled remedy, without initiating it.
3. If the user cannot or does not want to authenticate, answer from training knowledge and
   clearly note it may be outdated.

Never silently fall back to training data, always say why Context7 wasn't used.

For any lookup that affects implementation, record the selected library ID, indexed version (or
`latest indexed`), query, access mode (`MCP`, installed CLI, or `npx`), and whether the result
was exact-version or closest-version documentation.

## Common mistakes to avoid

- Library IDs require a `/` prefix, `/facebook/react` not `facebook/react`
- Always resolve first, `npx ctx7@latest docs react "hooks"` fails without a valid ID from the
  `library` step
- Use descriptive queries, not single words, `"React useEffect cleanup function"` not `"hooks"`
- One topic per query, split multi-concept questions into separate `docs` calls per concept,
  unless the question is specifically about how the concepts interact
- Never put sensitive information (API keys, passwords, credentials) in a query
