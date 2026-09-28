# Agent Adapters

The core workflow is host-neutral. MCP configuration, skill locations, target flags, and agent-specific
setup rules belong here rather than in the portable lookup logic.

## Adapter contract

Before setup or installation, identify:

1. target agent or host
2. target scope: project-local or user-global
3. documented configuration file or skill directory
4. whether the operation writes files, changes configuration, installs packages, or authenticates
5. how the target agent verifies that the configuration is active

Require explicit approval for each mutating operation.

## Current Context7 setup targets

The current upstream setup documentation includes dedicated target flags for some agents, including
Claude Code, Cursor, and OpenCode for MCP setup, plus target locations for CLI + Skills mode. Treat those
flags as versioned adapter data, not universal CLI syntax.

Examples documented upstream include:

```text
ctx7 setup --claude
ctx7 setup --cursor
ctx7 setup --opencode
ctx7 setup --cli --claude
ctx7 setup --cli --cursor
ctx7 setup --cli --universal
ctx7 setup --cli --antigravity
```

Do not assume a flag remains supported by every future CLI release. Verify `ctx7 setup --help` when the
installed version disagrees with the documented adapter.

## Generic portability rules

- Never assume `origin`, `main`, or a universal config path.
- Never infer a host-specific skill directory from the current working directory alone.
- Never copy a target flag from one agent into another agent's command.
- Keep secrets out of adapter configuration examples.
- Prefer the target agent's current documentation for final path and schema details.

## Unknown adapter

If the target agent is not documented by the available Context7 tooling, do not fabricate its config
shape. Identify the missing adapter information and stop before writing files.

## Post-setup verification

After an authorized setup operation:

1. inspect the exact files or configuration entries that changed
2. verify the target scope
3. confirm the Context7 server or skill is visible to the target agent when that check is available
4. report any part that could not be verified

A successful setup command is not proof that the target agent loaded the configuration.
