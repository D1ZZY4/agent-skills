# CLI Output Copy

Copy for command-line interfaces: help text, flag descriptions, deprecation warnings,
non-interactive errors, and progress lines. The same principles that apply to UI copy apply
here, but terminal output has tighter constraints and a different reading context.

## Help text and flag descriptions

- Name the command, what it does, and the state the user ends up in, in plain language.
  "Generates a build report from project metadata" beats "A tool".
- Describe each flag by its effect, not by restating its name. For an `--quiet` flag,
  "Suppress progress output" beats "Quiet mode".
- Show the flag's expected value with a placeholder that matches the project's convention,
  for example `--out <path>` or `--out=path`, and keep that placeholder consistent across
  every occurrence.
- Keep the whole help screen scannable: short descriptions, related flags grouped, a short
  example near the end.

## Non-interactive errors

Terminal errors follow the error-message pattern in `error-messages.md` (state what happened,
explain why when useful, give the next step) with tighter constraints:

- Lead with the failing fact, not a stack trace or internal symbol. Move reference IDs and
  trace details to a later line where support can use them.
- Match the message to the failing operation. A usage problem explains what to fix; it does
  not say "panic: unexpected error".
- Keep each line parseable: one clear sentence of meaning, no information carried only by
  color or ANSI styling. If color is used, the same meaning must hold when output is
  redirected to a file.
- Never print secrets, tokens, URLs with credentials, or whole environment dumps in error
  output.

## Deprecation warnings

- Say what is deprecated and what to use instead, with a version or date when known.
  "`--follow` is deprecated in 3.0, use `--tail` instead."
- Do not print deprecation noise on every run. Emit one clear warning at a point the user
  will see it.

## Progress and result lines

- Use a consistent, simple prefix symbol per state, and never rely on color or spinner
  animation alone: a failed step must still read as failed when output is captured to a log.
- End long-running operations with an explicit final state instead of silence.
- Keep lines reasonably short and avoid wrapping mid-token in log-friendly output.

## Localization and tone

- CLI strings are user-facing copy too. Translate and pluralize them with the same care as UI
  strings, using named placeholders such as `{count}` for values instead of relying on word
  order.
- Plain and precise; zero cleverness in errors and destructive confirmations, matching
  `voice-and-tone.md`.
- Follow the repository's em dash preference in generated help text and output.