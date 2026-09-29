# CLI Output Copy

User-facing copy for command-line interfaces, including help, flags, prompts, errors, progress, results, and deprecation notices.

## Help and usage

- Describe what the command does and the result or state it produces.
- Describe flags by effect, not by echoing the flag name.
- Match placeholder syntax to the project's existing CLI convention, such as `--out <path>` or `--out=path`.
- Keep usage scannable. Group related options and include a realistic example when useful.
- Preserve literal flags, environment variable names, commands, paths, and identifiers exactly. These are interfaces, not prose.
- Document defaults, required values, constraints, and mutually exclusive options when users need that information to invoke the command correctly.

## Errors

Use the same core pattern as `error-messages.md`:

1. state what failed in user terms
2. explain the cause when known and useful
3. give the next action when one exists

Do not lead with stack traces, internal function names, request payloads, or raw provider responses. Put diagnostic IDs or technical detail after the user-facing explanation when they are useful for support.

Never print secrets, access tokens, credential-bearing URLs, private keys, full environment dumps, or other sensitive values.

## Exit state and progress

- A long-running command should end with a clear success, partial-success, or failure state.
- Do not rely on color, spinners, symbols, or animation to communicate state. Output must remain meaningful when redirected to a file or captured in CI logs.
- If the command can partially succeed, state what completed and what remains.
- Avoid progress messages that imply completion before the operation actually finishes.
- Keep lines readable in narrow terminals and avoid breaking long identifiers unnecessarily.

## Deprecation

- Name the deprecated command or option and the replacement.
- Include a version or date only when verified.
- Avoid repeating the same warning on every invocation when a less noisy documented pattern exists.
- Do not claim removal timing unless the project has actually committed to it.

## Interactive prompts

For CLI prompts that can change or delete data:

- describe the affected object and consequence
- use a specific confirmation response when ambiguity matters
- never require users to infer what `y` or `n` means from hidden context
- preserve non-interactive behavior required by CI and scripting

## Localization and formatting

CLI output can be localized, but many tools intentionally keep commands, flags, and diagnostics stable across locales. Follow the project's established model rather than translating identifiers or machine-readable output.

Keep human-readable copy separate from machine-readable output when the CLI supports both. Stable parsers should not have to scrape prose intended for people.

## Unicode hygiene

Do not replace ASCII hyphens in flags, options, paths, or identifiers with typographic dash characters. For generated prose, follow the project punctuation policy in `formatting-and-punctuation.md`.
