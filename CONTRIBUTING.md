# Contributing

Everyone is welcome here. Whether you want to fix a typo, improve a skill, or propose a whole new one, your contribution matters to this repo.

An honest note first: this repository is still young and has plenty of rough edges. Only `context7-expert` has a full comparison against its upstream original so far; the same treatment for the other skills is still pending. Docs may be uneven and conventions are still settling. If you see a gap, that is not a reason to stay away. It is a reason to open an issue or send a pull request.

## Ways to contribute

- Improve an existing skill (`SKILL.md` or anything under its `references/`).
- Propose a new skill as a new directory.
- Fix docs (`README.md`, `CHANGELOG.md`, this file).
- Open an issue for bugs, unclear wording, or missing comparisons.

## Ground rules

Everything you need is in this file. No other rule file required.

- Change only what the task needs. Read freely, keep edits focused.
- Never invent tool behavior, versions, paths, or compatibility claims. Check the repo first.
- Do not use em dashes in docs, UI copy, or commit messages. Keep commands, flags, paths, and identifiers on their exact ASCII hyphens.
- Every notable change updates [CHANGELOG.md](CHANGELOG.md) under `[Unreleased]`, which always stays the first section.
- Skill versions (`metadata.version` in `SKILL.md`) and project versions (`1.Y.Z` headings in `CHANGELOG.md`) move independently. Never start a version with `0`.
- Every commit is signed. Unsigned commits are not accepted.

## Step by step

### 1. Fork and clone

Fork the repository on GitHub, then clone your fork:

```bash
git clone https://github.com/<your-username>/agent-skills.git
```

Replace `<your-username>` with your GitHub username.

### 2. Create a focused branch

Branch from `main` and keep one branch per change:

```bash
git checkout main
git pull origin main
git checkout -b <short-branch-name>
```

Keep the name short and descriptive, for example `fix-readme-typo` or `add-docker-skill`. There is no enforced naming scheme beyond that.

### 3. Make your change

Skill sources live in the tracked directories under `skills/` (`skills/context7-expert/`, `skills/copywriting-expert/`, and so on). The copies under `.agents/skills/` are local agent state, ignored by git. Do not edit those. Do not add anything under ignored paths such as `.local/`, `.cache/`, `.config/`, or `gpg-key-backup/`.

A skill is one directory with this shape:

```text
my-skill/
  SKILL.md
  references/
```

`SKILL.md` starts with frontmatter like this:

```yaml
---
name: my-skill
description: >
  One or two sentences saying what the skill does and when it loads.
license: SSPL-1.0
metadata:
  version: 1.0.0
  author: your-name
  priority: medium
---
```

Rules for the change itself:

- `SKILL.md` is the routing and safety layer. Detailed procedures go in `references/`, and the skill loads only the reference needed for the current step.
- Bump `metadata.version` when you change a skill. Project versions (`1.Y.Z` headings in `CHANGELOG.md`) and skill versions move independently. Never start a version with `0`.
- Follow the existing voice: clear, direct, developer-facing. No marketing filler, no cleverness where precision matters.
- Never paste secrets, tokens, or private keys into docs, queries, or commits.

### 4. Test locally

Copy or symlink the skill directory into a skills path your agent reads, then confirm the agent lists the skill and its trigger behaves as described. See the Setup section in [README.md](README.md). If you cannot test with a given agent, say so in the pull request instead of claiming you did.

### 5. Update the changelog

Add a bullet under `[Unreleased]` in [CHANGELOG.md](CHANGELOG.md) describing what changed and why. Group related edits into one bullet rather than listing every file.

### 6. Commit signed with a clear message

Stage only the files your change needs, never everything by habit:

```bash
git status --short
git add <file> <file>
```

Write the message in the repo's established style (type, short imperative subject, bullet body for non-trivial changes):

```bash
git commit -S -m "docs(readme): fix setup pointer" -m "- One line about what changed
- One line about why"
```

Common types in this history are `docs`, `feat`, `fix`, `refactor`, and `chore`, with an optional scope such as `docs(readme)`. Match the surrounding history rather than inventing a new format.

### 7. Push to your fork and open a pull request

```bash
git push origin <short-branch-name>
```

Then open a pull request against `main` of the upstream repo. In the description, state what changed, why, what you tested, and what you could not test. Keep the pull request focused: one concern per pull request, so it can be reviewed and reverted cleanly.

## Review expectations

- A maintainer reviews every pull request. Small doc fixes usually move fast; new skills get a closer read on triggers, safety boundaries, and wording.
- You may be asked to split an unrelated mix of changes, add a changelog bullet, or verify a claim against the repo. That is normal here, not a rejection.
- Be kind in comments, about your own work and others'. Direct technical feedback is welcome; dismissive tone is not.

## Opening an issue

Check open issues first to avoid duplicates. A good issue names the skill and file, quotes the confusing or wrong text, and says what you expected instead. Screenshots or exact commands help when the problem involves rendering or CLI output.

## License

Contributions land under the repo license, SSPL-1.0 (see [LICENSE](LICENSE)). New skills carry `license: SSPL-1.0` in their `SKILL.md` frontmatter, matching every existing skill.
