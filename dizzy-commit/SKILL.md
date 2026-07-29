---
name: dizzy-commit
description: >
  Enforce disciplined Conventional Commits and a clean working tree on every git commit.
  Use this skill whenever the user says "commit", "git commit", "push", "stage", "/commit",
  "caveman commit", "strict commit", "dizzy-commit", asks you to write, review, or fix a commit message, or
  when you are about to commit code and need to check the message follows the rules. Also use
  at the end of any coding session, before declaring a task done, to verify the working tree
  is clean. Fully self-contained: no external `.agents/rules` lookup needed. All rules,
  including the strict per-project variant (fixed author identity, banned words), live inside
  this skill's `references/` folder. Works the same way in every project. Swift DE, SIMPHAUL,
  TCF Bot, Catat Artha, Hermes Agent, or any new repo, out of the box.
---

# Dizzy Commit

Everything this skill needs is bundled here. No repo setup, no external rules file to check.

## Two modes

- **Default mode** (used automatically, always): the global rules below.
- **Strict mode**: triggered when the user says "strict commit", "strict mode", names a
  project known to require a fixed commit author (e.g. TCF Bot / D1ZZY4 repos), or explicitly
  asks to enforce author identity or banned-word rules. Read `references/strict-mode.md` for
  the extra constraints (fixed author, banned words, no amend-after-push) and apply them on
  top of the default rules below, not instead of them.

If unsure which mode applies, ask once, or default to the global rules. They're a safe
baseline either way.

## Step 1: Inspect the diff

```bash
git status --short
git diff            # unstaged
git diff --cached   # staged
```

Never write a commit message from memory or a plan/checklist. Always derive it from the
actual diff.

## Step 2: Group by logical concern

Group changed files by concern: one bug fix, one refactor, one feature, one docs update. If
the diff spans unrelated areas, split into multiple commits. Never bundle unrelated changes,
even if asked to "commit everything at once." Warn the user and offer to split; if they
insist, generate one commit per concern anyway.

## Step 3: Write the message

Format (Conventional Commits):

```
<type>(<scope>): <short imperative summary>

<body, required, markdown>
```

**Subject line**
- Scope is mandatory, not optional: `type(scope): summary`. Only skip the parentheses when
  the change genuinely touches the whole repo with no single module or area (a repo-wide
  dependency bump still gets `deps` as scope; a truly scope-less change is a rare exception,
  not the default).
- Pick the scope from the area actually changed: a module name, package, folder, feature, or
  component. Examples: `feat(api)`, `fix(auth)`, `docs(readme)`, `refactor(ui)`. Keep it
  short, lowercase, one word or short-hyphenated when possible.
- Imperative mood: "add", "fix", "remove", never "added", "adds", "adding"
- Short and punchy: aim 50 characters or less, soft cap around 72
- No trailing period
- No em dashes, ever. Not in the subject, not in the body, not anywhere in a commit message.
  Use a comma, colon, period, or parentheses instead.
- No emoji, ever. Not even if it seems fitting or the project uses them elsewhere.
- English only, always, regardless of the language the conversation is in

**Body: mandatory, always Markdown**
- Every commit gets a body. Never subject-only, even for small changes. Explain the why at
  minimum, in a sentence or two, even if the what is obvious from the diff.
- Must use Markdown formatting: bullets (`-`), inline code, bold, headers all fine. A body
  that is a single unformatted sentence is fine content-wise, but reach for Markdown structure
  (bullets, code spans) whenever there is more than one point to make.
- Explain what and why, not how.
- No em dashes and no emoji in the body either. Same rule as the subject line.
- Wrap prose around 72 characters.
- Reference issues at the end when relevant: `Closes #42`, `Refs #17`.
- Breaking changes, security fixes, data migrations, and reverts always get a fuller body.
  Never compress these into a one-liner.

**Never include:**
- "This commit does X", "I", "we", "now", "currently"
- "As requested by...", use a `Co-authored-by` trailer instead
- "Generated with Claude Code" or any AI attribution
- Any emoji, under any circumstance
- Any em dash, under any circumstance
- The words `phase`, `session`, `iteration`, `step`
- Generic AI summaries like "Update documentation" or "Address findings from audit"

### Commit type reference

| Type | When to use |
|------|-------------|
| `feat` | New feature or behaviour |
| `fix` | Bug fix |
| `chore` | Tooling, config, deps. No production code change |
| `docs` | Documentation only |
| `refactor` | Restructure without behaviour change |
| `style` | Formatting, whitespace. No logic change |
| `perf` | Performance improvement |
| `test` | Adding or fixing tests |
| `build` | Build system or dependencies |
| `ci` | CI configuration |
| `revert` | Reverting a prior commit |

Breaking change: append `!` after type/scope, explain in body with `BREAKING CHANGE: ...`.

## Step 4: Verify before committing

Run whatever verification the project actually has (check `package.json` scripts, `Makefile`,
etc.). Common defaults: `pnpm typecheck`, `pnpm lint`, `pnpm build`. If any fail, report the
errors and do not commit until fixed. Skip silently only if the project has none of these set
up.

## Step 5: Stage, commit, clean the tree

1. Stage only the files for the current concern (`git add <file>`), not `git add -A` unless
   the whole diff really is one concern.
2. In strict mode, set author per `references/strict-mode.md` and verify with
   `git log -1 --format="%an <%ae>"` before pushing.
3. Commit: `git commit -m "type(scope): summary" -m "body"`. Scope and body are both required.
4. Repeat per concern.
5. Before declaring the task or session done, always run:
   ```bash
   git status --short
   ```
   Output must be empty. Every remaining file is either committed or intentionally discarded
   (`git checkout -- <file>` / `git clean -fd`). No "trivial leftover" exception. An
   unattended platform (Replit, CI, etc.) may otherwise auto-commit leftovers with a message
   that violates every rule above.

## Anti-patterns to reject

Reject and rewrite any commit message (yours or the user's) that:

- Has no scope, i.e. `type: summary` with no `(scope)` and no genuine repo-wide justification
- Has no body at all, i.e. subject-only with nothing explaining the why
- Contains an em dash anywhere in the subject or body
- Contains an emoji anywhere in the subject or body
- Isn't written in English
- Contains `phase`, `session`, `iteration`, `step` (including numbered variants)
- Uses past tense instead of imperative
- Ends with a period
- Is a generic AI summary instead of describing the real change
- Bundles unrelated changes with no logical connection
- Describes implementation details in the subject instead of the body
- Writes the body as a wall of plain text when Markdown would be clearer
- Leaves the working tree dirty after the "done" declaration

## Caveman mode

On "caveman commit", "/caveman-commit", or "terse commit": compress the body to the bare
minimum, one Markdown line or one short bullet stating the why, but never drop it entirely.
Body is still mandatory. Breaking changes, security fixes, migrations, and reverts still get a
fuller body regardless of mode. Same format, scope requirement, and banned words and
characters (em dash, emoji) still apply. In caveman mode, only output the message as a code
block, don't stage or commit. "stop caveman-commit" or "normal mode" reverts to the full
Step 1 through 5 workflow.

## Examples

**Default mode:**
```
feat(api): add GET /users/:id/profile

Mobile client needs profile data without the full user payload
to reduce LTE bandwidth on cold-launch screens.

Closes #128
```

**Strict mode** (two unrelated dark-mode fixes, split into two commits, see
`references/strict-mode.md` for the author and banned-word rules applied here):
```
fix(button): dark mode contrast on danger variant

Add `dark:text-[#f07060]` and `dark:border-[#d44a30]` to danger variant.

Aligns with `--status-unstable-text` and `--status-unstable-border` dark
variants already defined in `globals.css`.
```
```
fix(info-tab): status tokens for stable/bug colors

- `text-[var(--color-stable)]` -> `text-[var(--status-stable-text)]`
- `bg-[var(--color-unstable)]` -> `bg-[var(--status-unstable-border)]`

Fixes dark mode contrast. The raw color vars have no dark override.
```

**What NOT to do** (bundled, plan-flavored, banned words):
```
refactor: Phase 3, security fixes, bug fixes, and accessibility improvements

Security:
- Remove spam-protection note from FeedbackForm
- Add URL scheme guards for download_link/donate_link
...
```
17 unrelated changes in one commit, no scope, contains "Phase 3." Split into one focused
commit per concern instead, each with its own scope.

## Bundled references

- `references/strict-mode.md`: fixed commit author, banned-word list, and no-amend rule for
  projects that require it (e.g. D1ZZY4 / TCF Bot conventions). Read only when strict mode
  applies.
- `references/clean-tree-checklist.md`: the full end-of-session checklist, if you want more
  detail than Step 5 above gives.
