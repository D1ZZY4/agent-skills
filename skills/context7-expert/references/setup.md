# Setup

Use only when the user explicitly asks to install, configure, authenticate, or remove Context7 setup for
an editor or coding agent. A documentation question alone does not authorize setup.

## Supported setup modes

The current upstream CLI documents two setup modes:

- **MCP**: configure a Context7 MCP server for the target agent.
- **CLI + Skills**: install a `find-docs`-style skill that guides the agent to use the `ctx7` CLI.

Reference command shapes:

```text
ctx7 setup
ctx7 setup --mcp
ctx7 setup --cli
ctx7 setup --project
```

Target flags and paths are host-specific. See `agent-adapters.md` and verify against the installed CLI's
help when necessary.

## Authentication

The current upstream setup flow supports browser-based OAuth and API-key-based authentication. Login,
OAuth, logout, and credential changes are separate user actions.

Security rules still apply:

- never ask for a real API key in chat
- never paste a real key into a command or committed file
- prefer the host's secret store or supported environment/credential mechanism
- do not run setup merely because a normal documentation lookup failed

The upstream CLI currently documents `ctx7 login`, `ctx7 logout`, and `ctx7 whoami`. Treat login/logout
as mutations of authentication state and `whoami` as an inspection command unless the installed CLI
documents otherwise.

## Confirmation before setup

Before running setup, confirm:

- target agent
- MCP or CLI + Skills mode
- project-local or user-global scope
- expected files/configuration entries
- authentication method, if needed
- any package execution path such as `npx`

Do not use `--yes` by default. Skipping confirmation is itself a user-controlled choice.

## What may be written

MCP setup can write an MCP server entry and related Context7 rule or skill files. CLI + Skills setup can
write a `find-docs`-style skill.

The exact file names and locations are host-specific. Do not assume the paths shown by another agent
integration apply here.

## Post-setup verification

After an authorized setup:

1. inspect the files or config entries actually written
2. verify the requested scope
3. verify the target agent can see the configuration when possible
4. record any generated or modified files
5. report failures honestly

A setup command returning success does not by itself prove the agent is connected or authenticated.

## Removal

Removal is also a mutation. Confirm the exact generated files or configuration entries to remove before
running a removal command.

Never delete unrelated configuration merely because it was adjacent to Context7 setup.

## Sources checked

- https://github.com/upstash/context7/tree/master/packages/cli
- https://github.com/upstash/context7/tree/master/skills/context7-cli
- https://github.com/upstash/context7/tree/master/skills/context7-cli/references/setup.md
