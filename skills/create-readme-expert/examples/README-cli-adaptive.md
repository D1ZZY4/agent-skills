# CLI Tool Name

## Repository evidence

Found:
- package.json bin field maps to ./bin/cli.js
- src/cli.js defines commands: init, build, deploy
- README previously omitted the deploy command

## README decisions

Include:
- installation method from package manager
- init, build, and deploy commands with verified flags
- troubleshooting for deploy exit code 1 found in CI logs

Do not include:
- hypothetical future commands
- unsupported platform-specific flags
