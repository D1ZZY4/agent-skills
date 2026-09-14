# Alert Callouts in READMEs

GitHub-style blockquote alerts for security notes, warnings, and focused callouts.
Renderer-specific, so confirm the platform before using them.

## Repository evidence

- The README will be rendered on GitHub, which supports alert syntax.
- The project exposes tokens, database URIs, and webhook secrets as environment variables.
- The project can be deployed to hosted platforms with a secret manager.

## README decisions

Include:
- `> [!IMPORTANT]` for credentials and anything that must never reach the repository.
- `> [!WARNING]` for behavior users commonly get wrong.
- `> [!CAUTION]` for actions with destructive or irreversible consequences.
- `> [!NOTE]` and `> [!TIP]` only for asides that a plain paragraph would bury.

Do not include:
- Alerts for content a normal paragraph covers just as well.
- Alert syntax when the primary renderer does not support it.
- Placeholder values that look like real configuration.

## Bad README

"Put the bot token in the .env file and it just works."

## Correct README

## Configuration

Copy `.env.example` and fill in the values.

```bash
cp .env.example .env
```

> [!IMPORTANT]
> Never commit real secrets. Keep `BOT_TOKEN`, `MONGODB_URI`, passwords, webhook secrets,
> and private chat IDs out of the repository. Use the platform secret manager on hosted
> deployments.

> [!WARNING]
> The bot replies in every channel it can read. Start it in a private test channel before
> granting broader access.

> [!CAUTION]
> `delete-all` removes every message from the channel. It cannot be undone.

## Source of truth

Name only environment variables that exist in the project manifest, example env files, or
CI configuration. Do not invent token names or access scopes. See
`references/verification-and-failure.md` when a variable's purpose is unconfirmed.

## Renderer compatibility

Alert syntax is a GitHub-flavored Markdown feature. On GitLab, npm, or other renderers,
the `> [!IMPORTANT]` line renders as a plain blockquote, so only use it when GitHub is the
README's primary host, or verify the target renderer first.