# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

[Detailed Changelog](#per-skill-changelog)
---

## [Unreleased]

### copywriting-expert

- Bumped metadata.version to 1.9.0.
- Rewrote the workflow around the distinction between copy content and copy
  implementation. Accessibility and localization remain content requirements, but
  copy alone cannot certify focus management, semantics, or announcement
  behavior, so the skill now flags implementation defects instead of implying a
  string change fixes them.
- Add an operating-modes table separating draft, rewrite, audit, implementation,
  and review, each with its own mutation boundary, so an audit is not read as
  permission to rewrite.
- Add principles for preserving placeholders, variables, product names, and
  markup exactly, and for treating user-controlled data as data so secrets in an
  error or example are never reproduced.
- Expand the empty-state reference into a six-state table that separates genuine
  absence from filters, user actions, permission limits, loading, and fetch
  failure, so a failed request cannot be reported as an empty workspace.
- Expand the component reference with a list of non-display uses for a string,
  including analytics identifiers, localization keys, test fixtures, and parser
  input, so a rename is not treated as presentation-only.
- Add a `partially verified` evidence state and separate accessibility and
  localization verification into distinct questions.
- Add a `Confidence and claims` section to the voice reference covering
  unverified guarantees such as `always`, `instant`, and `fully secure`.
- Note the two rules dropped from `verification-and-failure.md` in review: the
  instruction to record assumptions that materially affect the output, and the
  requirement to obtain authorization when verification would cause a side
  effect. Neither is stated anywhere in the rewritten file.

## [1.16.0] - 2026-09-29

<details>
<summary>1.16.0 - 2026-09-29</summary>

### Repository

- Grouped plugin manifests per host so each agent reads its own file: moved the
  portable Agent Plugins manifest from the repository root to
  `.agents/plugins/plugin.json`, added `.codex-plugin/plugin.json` as the Codex
  native manifest, and left `.claude-plugin/` and `.cursor-plugin/` at the paths
  their specs require.
- Replaced `.cursor-plugin/marketplace.json` with `.cursor-plugin/plugin.json`.
  The marketplace listed seven entries whose `source` paths had no matching
  per-plugin manifest, so Cursor skipped the manifest step for every entry and
  the per-skill `version`, `category`, and `tags` never took effect. It also
  made the documented `/add-plugin agent-skills` command unresolvable, because
  no entry carried that name. One plugin bundling every skill matches how the
  Claude, Gemini, and Agent Plugins channels already treat this repository, and
  Cursor finds the skills through default `skills/` discovery. Install a single
  skill in Cursor through `npx skills add --skill <name>`.
  Per-skill `category` and `tags` are dropped with the marketplace; each
  `SKILL.md` keeps its own `name` and `description` frontmatter.
- Added a Plugin manifests table to `README.md` recording the manifest, the host
  that reads it, and the spec it follows.
- Added `!.agents/plugins/` to `.gitignore` so the relocated manifest stays
  tracked while the rest of `.agents/` remains ignored local state.
- Known regression: GitHub Copilot reads the Agent Plugins manifest at the
  repository root, so it no longer discovers this repository. Codex still works
  through `.codex-plugin/plugin.json`. Restoring a root `plugin.json` is a
  one-line fix if Copilot support is needed.
- Ignored `art/` and `skills-lock.json` as local working state.
- Documented why Cline has no row in the manifest table. A Cline plugin is a
  TypeScript or JavaScript module exporting an `AgentPlugin`, discovered through
  a `cline` field in `package.json` or a scan for `.ts` and `.js` files, so a
  repository of markdown `SKILL.md` files has no manifest to publish.
  `cline skill install` remains the supported path and takes the same
  `--skill` flag.
- Correct three claims in the documentation. The `### Repository` row for
  Codex now names the `.claude-plugin/plugin.json` fallback instead of
  repeating the manifest path, the deep-research-expert sources paragraph no
  longer ends on a dangling "the same way", and `caveman-commit`-style takes
  the hyphen it needs as a compound modifier.
- Removed a phantom `context7-expert` 1.5.0 row from the per-skill table. The
  row's description was a verbatim copy of the 1.2.0 row. Added the 1.6.0 and
  1.9.0 rows the table was missing, sourced from the 1.6.0 and 1.8.0 release
  sections. Version 1.4.0 remains absent because no commit ever carried it.
- Reconstructed ten per-skill version rows that the tables had lost, by
  replaying `metadata.version` across all 151 commits. The skills lived at the
  repository root before the move into `skills/`, which is why the gap was not
  visible from the current tree. Restored: `context7-expert` 1.5.0, 1.7.0,
  1.7.1, and 1.8.0; `copywriting-expert` 1.3.1; `create-readme-expert` 1.7.0,
  1.9.0, and 1.12.0; `mermaid-diagrams-expert` 1.2.1; and `redis-expert` 1.2.0.
  Every restored row is dated and described from the commit that introduced
  that version, not inferred.

### context7-expert

- Bumped metadata.version to 1.14.0.
- Replaced the `Priority order` section with `Core principles` and
  `Authorization model`, matching the structure `commit-expert` adopted in
  1.18.0. The existing five-level conflict resolution is kept inside the
  authorization section.
- Added `Failure handling` covering failed lookups, including the rule that a
  failed lookup is a valid outcome while an invented answer is not.
- Standardized `references/proactive-trigger.md` on the four sections every
  skill now uses: when to act, when to stay quiet, confidence rule, and how to
  offer. Added the missing stay-quiet section, covering an explicit decline in
  the same conversation and an answer already present in local project files.
- Bumped metadata.version to 1.15.0.
- Rewrote the workflow to separate five distinct version facts: declared,
  resolved, installed, Context7 indexed, and vendor current release. The
  previous version treated them as interchangeable, so a Context7 result could
  be read as proof of what the project actually runs.
- Require confirmation of the final redacted query that will actually be
  transmitted, not merely the user's original wording, and state that any retry
  which changes the transmitted query needs a new confirmation.
- Split the authorization table so "go ahead" covers only the proposed lookup
  batch, and added a separate row for "use the latest docs", which authorizes the
  version strategy only after the library and final query are shown.
- Added provenance fields to retain for implementation-affecting answers:
  library ID, indexed version, exact query, access mode, and lookup date.
- Tightened the reference set: per-shell CLI probes for PowerShell and cmd.exe,
  an explicit npx execution boundary, and separate rule-precedence and
  stop-condition sections.
- Updated the `context7-expert` comparison block in `README.md`. The how-it-works
  list described a six-step flow while the skill now runs nine, and three table
  rows still described the pre-1.15.0 consent, version, and provenance behavior.
  The reference count and every claim about upstream were left unchanged because
  they remain accurate.
- Renamed the `Priority order` heading in
  `commit-expert/references/policy-configuration.md` to match the same heading
  in its `SKILL.md`.

### copywriting-expert

- Bumped metadata.version to 1.8.0.
- Standardized `references/proactive-trigger.md` on the four sections every skill now uses. The new confidence rule separates a real defect from a register preference, and the stay-quiet section covers a project with no established voice when a draft was requested.
- Added `Core principles`, `Authorization model`, and `Failure handling`
  sections to match the `commit-expert` structure. The authorization table
  scopes an edit to the surface the request names instead of a silent sweep of
  the interface.

### create-readme-expert

- Bumped metadata.version to 1.15.0.
- Standardized `references/proactive-trigger.md` on the four sections every skill now uses, with one added confidence bullet noting that a stale-looking README is not automatically a wrong README.
- Added `Core principles`, `Authorization model`, and `Failure handling`
  sections to match the `commit-expert` structure. The operation-to-scope table
  makes an audit distinct from a rewrite, and the failure section keeps "the
  README is already accurate" as a valid outcome.

### deep-research-expert

- Bumped metadata.version to 1.6.0.
- Standardized `references/proactive-trigger.md` on the four sections every skill now uses. The new confidence rule requires the offer to earn its keep and forbids proposing a mode heavier than the question needs.
- Added `Core principles`, `Authorization model`, and `Failure handling`
  sections to match the `commit-expert` structure. The authorization table
  separates finding issues from fixing them, and the failure section covers
  unverifiable claims without inventing a substitute source.
- Kept `Safety boundary` alongside the new sections because it carries network
  transmission rules that do not fit the authorization table.

### mermaid-diagrams-expert

- Bumped metadata.version to 1.6.0.
- Standardized `references/proactive-trigger.md` on the four sections every skill now uses, and dropped the bold-label bullet style used in the trigger list.
- Added `Core principles`, `Authorization model`, and `Failure handling`
  sections to match the `commit-expert` structure. The failure section records
  that unrecognized config options are ignored silently, so a diagram can
  appear to render while the intended style was never applied.

### redis-expert

- Bumped metadata.version to 1.5.4.
- Updated the non-reference content note to point at `.cursor-plugin/plugin.json`
  instead of the removed `.cursor-plugin/marketplace.json`.
- Bumped metadata.version to 1.6.0.
- Standardized `references/proactive-trigger.md` on the four sections every skill now uses. The file previously ended without any offer guidance, so a how-to-offer section was added that names the single relevant domain instead of listing all eight.
- Added `Core principles`, `Authorization model`, and `Failure handling`
  sections to match the `commit-expert` structure. The authorization table
  separates advisory work from operations that reach a live deployment.
- Kept the domain sections as the body after `Step 1`, since this skill routes
  by domain rather than running a linear workflow.

### commit-expert

- Bumped metadata.version to 1.18.0.
- Restructured `SKILL.md` from six steps to eight and replaced the loose
  authorization wording with an operation-specific table mapping each user
  instruction to the side effects it covers. "commit" no longer implies "push",
  and "push" no longer implies "create a commit".
- Added detection for in-progress merge, cherry-pick, revert, and rebase state,
  so an ordinary task commit is never created on top of an active operation.
- Added a status vocabulary to `verification-and-failure.md` covering
  `skipped` and `not applicable` alongside the existing not-checked, passed, and
  failed states, and a section separating verification from authorization.
- Widened signature and pre-push checks from the latest commit only to the full
  range that will be pushed, and documented that a local signature result does
  not imply a provider displays a verified badge.
- Documented that `git push -u` changes tracking configuration, so it is not
  used as a hidden side effect of an ordinary push.
- Added submodule and nested-repository scope handling, generated-file guidance,
  and an explicit ban on `git add -f` for ignored files in
  `staging-and-gitignore.md`.
- Known issue: the sentence in `commit-execution.md` warning against literal
  `\n` in a shell string lost its escape sequence during editing, leaving a
  stray backtick and a split sentence. The rule still reads correctly, but the
  example it referred to is gone. The worked failure examples in
  `examples.md` were also dropped, leaving that reference with good-case
  examples only.

</details>

---

## [1.15.0] - 2026-09-18

<details>
<summary>1.15.0 - 2026-09-18</summary>

### deep-research-expert

- Bumped metadata.version to 1.5.0.
- Added auto default mode plus eight modes (Spot, Standard, Deep, Forensic,
  Comparative, Adversarial, Exhaustive, Decision) with depth chain versus
  specialized split, per-mode stopping rule, evidence requirement, query strategy,
  and reporting add-on in `references/depth-modes.md`.
- Updated SKILL.md Step 0 to auto resolution, Steps 1 to 4 to per-mode routing,
  and the bundled references list.
- Updated `references/proactive-trigger.md` with mode-aware triggers and offers
  while keeping the house headings (When to act, When to stay quiet, How to offer).
- Extended `references/critique.md` with an Adversarial falsification checklist,
  `references/evidence-grading.md` with symmetry plus falsification plus coverage
  plus traceability add-ons, `references/report-format.md` with per-mode add-ons
  and auto to X methodology, `references/source-ladder.md` with coverage targets
  and provenance notes, `references/quality-checklist.md` with mode hygiene, and
  `references/verification-and-failure.md` with mode-specific checks.
- Clarified `references/code-review.md` precedence: two-axis flow wins for review
  tasks, depth mode sets rigor only.
- Synced `.cursor-plugin/marketplace.json` deep-research-expert to 1.5.0 with
  comparison and decision findability.
- Bumped metadata.version to 1.5.1.
- Removed the `Sources checked` upstream-attribution block from
  `references/code-review.md` per owner instruction; flow, smell baseline, and
  grading cross-links unchanged.
- Synced `.cursor-plugin/marketplace.json` deep-research-expert to 1.5.1.
- Bumped metadata.version to 1.5.2.
- Removed the `Sources checked` quality-gates attribution from
  `references/quality-checklist.md` per owner instruction.
- Synced `.cursor-plugin/marketplace.json` deep-research-expert to 1.5.2.

### mermaid-diagrams-expert

- Bumped metadata.version to 1.5.1.
- Trimmed generic web content from `references/advanced-features.md`: removed the
  Responsive Sizing CSS snippet, SVG Export Options (covered by
  `references/validation-and-rendering.md`), and the Integration Examples section
  (Markdown, HTML, and React boilerplate).
- Synced `.cursor-plugin/marketplace.json` mermaid-diagrams-expert to 1.5.1.

### redis-expert

- Bumped metadata.version to 1.5.2.
- Removed the summary-level `13. LLM primitives` section from
  `references/search/clients/python-redisvl.md` (deferred coverage by its own text);
  kept the section 1 routing signal and the upstream index entries, renumbered the
  two following sections.
- Synced `.cursor-plugin/marketplace.json` redis-expert to 1.5.2.
- Bumped metadata.version to 1.5.3.
- Removed the upstream `iris-development` attribution blocks from the four
  `references/iris/` files and the whole-skill origin note from `SKILL.md` per
  owner instruction; kept the runtime-authority rule sentence.
- Synced `.cursor-plugin/marketplace.json` redis-expert to 1.5.3.

### Repository

- Synced the README Skills table (redis agent memory, deep-research comparisons
  and decisions) and the deep-research compare block (auto plus eight modes)
  with the current skill state.
- Expanded `plugin.json` keywords with `comparison`, `decision`, and `forensic`
  to mirror the Cursor marketplace tags for deep-research-expert.

</details>

---

## [1.14.0] - 2026-09-15

<details>
<summary>1.14.0 - 2026-09-15</summary>

### commit-expert

- Bumped metadata.version to 1.17.1.
- Added the Conventional Commits specification source to
  `references/message-style.md`.

### deep-research-expert

- Bumped metadata.version to 1.4.0.
- Added `references/quality-checklist.md`: pre-delivery checks for truncation,
  placeholders, citation hygiene, fact-versus-synthesis marking, and density.
- Added outline check to `references/depth-modes.md` and counterevidence plus
  metadata footer plus long-report delivery to `references/report-format.md`.
- Wired the checklist into SKILL.md Step 4.
- Added `references/code-review.md`: two-axis review (Standards vs Spec) against
  a fixed point, smell baseline, and critique loop, adapted from
  mattpocock/skills code-review and 199-biotechnologies/claude-deep-research-skill.
- Added `references/depth-modes.md` (Spot, Standard, Deep) and
  `references/critique.md` (three personas, delta queries, one-round stop rule).
- Extended `references/source-ladder.md` with retrieval discipline (date check,
  parallel fetches, structured notes, dedup by origin).
- Review-mode routing: description triggers on code review, Step 4 defers to the
  code-review aggregate format, trigger covers review tasks with fixed point
  and spec source up front.
- Large-diff guard in `references/code-review.md`; mode-switch rule in
  `references/depth-modes.md`; downgrade cross-link in
  `references/evidence-grading.md`.
- Added a pair-to-compare README block for deep-research-expert and source links
  to the context7-expert compare block.

</details>

---

## [1.13.0] - 2026-09-15

<details>
<summary>1.13.0 - 2026-09-15</summary>

### Repository

- Expanded `plugin.json` keywords from 20 to 32 and per-plugin Cursor
  marketplace tags so every skill is findable by feature terms (library-docs,
  mcp, ux-writing, microcopy, onboarding, flowcharts, c4,
  conventional-commits, caching, clustering, review, verification).
- Added project-level Cursor plugin marketplace at `.cursor-plugin/marketplace.json`
  covering all seven skills with per-skill versions, categories, and tags.
- Removed the per-skill `.cursor-plugin/` packaging from `skills/redis-expert/`
  (merged manifest plus seven upstream per-domain manifests); Cursor packaging now
  lives in one place at the repository root.

### redis-expert

- Bumped metadata.version to 1.5.1.
- Dropped the per-skill `.cursor-plugin/` packaging pointers from `SKILL.md`
  following the move to project-level Cursor packaging.

</details>

---

## [1.12.0] - 2026-09-15

<details>
<summary>1.12.0 - 2026-09-15</summary>

### deep-research-expert

- New skill at version 1.0.0 (initial experimental release, expect iteration as
  audit feedback lands): `SKILL.md` plus `references/proactive-trigger.md`,
  `references/source-ladder.md`, `references/evidence-grading.md`,
  `references/verification-and-failure.md`, and `references/report-format.md`.
  Codifies the deep audit workflow: full-scope reading, source ladder with
  `context7-expert` routing, two-source evidence grading, and severity-ranked reports.
- Registered in README Skills table, `skills.sh.json` (new Research and analysis
  group), and `plugin.json` keywords (`research`, `audit`).

### context7-expert

- Bumped metadata.version to 1.13.1.
- Added Node.js 18 prerequisite to `references/cli-mode.md` plus official source links.
- Added `npx ctx7 remove` and the manual MCP server URL to `references/setup.md`.
- Softened alias claims in `references/cli-skills-management.md`: confirm with `--help`
  since aliases shift between CLI releases.

### copywriting-expert

- Bumped metadata.version to 1.7.1.
- Clarified in `references/cli-output-copy.md` that the em dash ban is the strong
  default when no project rule exists.
- Added official source links (KBBI, EYD, Merriam-Webster, Oxford) to
  `references/language-and-vocabulary-verification.md`.

### create-readme-expert

- Bumped metadata.version to 1.14.1.
- Verified all four `references/external-readme-sources.md` URLs live with per-URL
  checked dates and a re-check note.
- Added the GitHub alerts docs source to `references/formatting-and-punctuation.md`.

### redis-expert

- Bumped metadata.version to 1.5.0.
- Added `references/iris/` domain (setup-and-auth, session-memory, long-term-memory,
  promotion): Iris Agent Memory now covered, matching upstream `iris-development`.
- Added `references/search/vector-sets.md`: native VADD/VSIM similarity search with
  quantization, filters, and Vector Set vs FT index guidance.
- Fixed `references/search/dialect.md`: dialects 1, 3, 4 are deprecated but functional
  with DIALECT 1 still the server default; explicit DIALECT 2 remains required.
- Migrated all `redis.io` search links from the retired `/develop/interact/` prefix to
  `/develop/ai/`.
- Added HEXPIRE 7.4 gate to the Hash row and refreshed the Cursor plugin manifest
  keywords for the new domain.

### mermaid-diagrams-expert

- Bumped metadata.version to 1.5.0.
- Added `references/new-diagrams.md`: venn-beta, ishikawa-beta, kanban, packet, radar-beta,
  treemap, plus mindmap, timeline, journey, sankey, block, quadrant, and requirement guidance
  with version minima, beta rules, and official docs sources.
- Added `references/security.md`: secrets handling, injection risks around click, classDef,
  and config, plus local validation guidance.
- Updated `SKILL.md`: expanded type table, beta fallback rule, security check in Step 4,
  removed informal wording, wired new references.
- Updated `references/diagram-type-selection.md`, `references/validation-and-rendering.md`
  (v11.13.0 label fix), and `references/renderer-adapters.md` (platform matrix and version minima).

### Repository

- Expanded `plugin.json` keywords from 8 to 18 so each skill is searchable by its
  own terms: `context7` and `api-docs` for docs lookup, `commit` and `workflow`
  for Git safety, `architecture` for diagrams, plus `vector-search`, `rag`,
  `semantic-cache`, `agent-memory`, and `iris` for the redis-expert 1.5.0 domains.
- Removed the replit.md symlink and polished AGENTS.md: full six-skill overview,
  complete structure map, no stale claims, tighter professional wording.
- Fixed skills.sh.json grouping: redis-expert moves to a new Infrastructure and data
  group matching the README category, added the missing mermaid keyword to plugin.json.
- Restyled all twelve agent logo tiles with a unified macOS tile system
  (vertical gradient plus top gloss highlight, corner radius kept at 24 percent).
- Tidied logo tile code (one element per line) and neutralized the tile
  gradient foot to authentic white #F2F2F7.

</details>

---

## [1.11.0] - 2026-09-14

<details>
<summary>1.11.0 - 2026-09-14</summary>

### create-readme-expert

- Bumped metadata.version to 1.14.0.
- Added `references/diagrams.md`: use `mermaid-diagrams-expert` when the README needs
  a diagram, with a canonical raw URL fallback when the skill is not installed.
- Wired the new reference from Step 4 and the Bundled references list.

### Repository

- Added official agent channels: Claude marketplace (`.claude-plugin/`), Agent Plugins
  manifest (`plugin.json`, shared by Cursor, Codex, and Copilot), and Gemini
  extension (`gemini-extension.json`), plus a README channel guide.
- Renamed `dizzy-commit` to `commit-expert` to match the `*-expert` convention.
  Skill version stays 1.17.0; rename only, no behavior change.
- Unified the Hermes tile corner radius with the other logos (24 percent).
- Moved all six skills into the standard `skills/` container directory (no functional
  change; skill names and discovery are unchanged).
- Added `CONTRIBUTING.md`: self-contained contributor guide for humans (fork, branch,
  test, changelog, signed commit, pull request), with no pointer into agent rule files.
- Added `assets/logos/` with verified agent logos and turned README Compatible agents
  into a collapsible single-column table (added Amp, Antigravity, Codex, Pi, Windsurf).
- Upgraded logos to colored brand marks where they exist: Claude starburst, Gemini
  gradient, multicolor Google G, official Cline bot mark, and a traced Hermes SVG.
- Moved the agent logos to a centered single-line strip under the skills.sh badge
  and removed the separate Compatible agents section.
- Put every logo on a white rounded tile for a uniform look and dark-mode safety.
- Removed the Design principles and Versioning sections from README; that content lives
  in `AGENTS.md` and duplicated it added noise for human readers.
- Fixed a wrong audience pointer in README Setup: replaced the `AGENTS.md` link (agent
  working rules) with a pointer to each skill's own `SKILL.md` for human readers.
- Polished README with `create-readme-expert` (Improve) and `copywriting-expert`:
  - fixed `context7-expert` reference count from 9 to 10 to match `skills/context7-expert/references/`
  - corrected the "Why these skills" intro so only `context7-expert` claims a full upstream comparison
  - clarified Packaging and License rows against upstream `upstash/context7` (MIT)
  - added a Skills index table and a two-path Setup section (preferred `npx skills add`, manual copy or symlink)
- Added a "Why these skills" README section comparing each skill against its original, framed
  around how the skill works, why it is worth it, the differences from the official version,
  strengths and weaknesses, and proactive loading. The context7 comparison is a collapsible
  block with a per-category table against the official `upstash/context7` layout (three skills
  plus two rules files) using HTML symbols for coverage markers; the other skills are pending.
- Linked the six skill names in the README Skills table to their relative
  `skills/<name>/SKILL.md` files and added a raw skill file URL pattern for
  harnesses that install from a URL.
- Polished README and CONTRIBUTING copy: centered the tagline, tightened install
  and channel wording, aligned setup terms, removed duplicated version rules.
- Made the README compare section generic and neutral: the intro no longer singles
  out one skill, entries follow as comparisons are completed, personal phrasing removed.
- Synced all marketplace manifest descriptions with the new README tagline so no
  fixed skill list rots as skills are added.

</details>

## [1.10.0] - 2026-09-13

<details>
<summary>1.10.0 - 2026-09-13</summary>

### create-readme-expert

- Bumped metadata.version to 1.13.0.
- Modernized the proactive trigger reference: consistent headings, a how-to-offer section,
  and bullet capitalization fixes.
- Bumped metadata.version to 1.12.0.
- Added a Purpose section to SKILL.md for a consistent, modern skill opening.
- Bumped metadata.version to 1.11.0.
- Added examples/README-github-alerts.md showing GitHub-style alert callouts (IMPORTANT, WARNING, CAUTION, NOTE, TIP) for secrets and destructive actions, with renderer compatibility notes.
- Added Callout blocks section to references/formatting-and-punctuation.md.
- Added the alerts example to the SKILL.md Step 4 always-use list and examples index.
- Bumped metadata.version to 1.10.0 in response to Snyk W011 (third-party content exposure / indirect prompt injection risk).
- Added user consent requirement before fetching any external README from references/external-readme-sources.md.
- Added references/security.md with W011 and indirect prompt injection rules.
- Added anti-pattern for fetching external READMEs without user confirmation.

### copywriting-expert

- Bumped metadata.version to 1.7.0.
- Modernized the proactive trigger reference: consistent headings (When to act, When to stay
  quiet, How to offer), fixed comma splices, and tightened the offer guidance.
- Bumped metadata.version to 1.6.0.
- Added a Purpose section to SKILL.md for a consistent, modern skill opening.
- Bumped metadata.version to 1.4.0.
- Added references/cli-output-copy.md for terminal surfaces: help text, flag descriptions, deprecation warnings, non-interactive errors, and progress lines.
- Extended SKILL.md description and Step 1 routing to cover CLI output copy.
- Added lookup hygiene rules (bare-term queries, consent when the term carries sensitive context) to references/language-and-vocabulary-verification.md.
- Added link text and alternative text guidance to references/accessibility-and-localization.md.
- Fixed broken " copy" placeholder token in references/examples-and-anti-patterns.md.
- Removed YAML frontmatter from references/toasts-and-onboarding.md to match the other references.
- Bumped metadata.version to 1.5.0.
- Added anti-AI-sounding patterns and domain adaptation guidance to references/voice-and-tone.md.
- Expanded references/project-source-of-truth.md with de facto house voice discovery (codebase strings, README, docs).
- Made reading existing project copy a required first step in SKILL.md Step 0.
- Added navigation copy guidance to references/ui-component-copy.md.
- Added loading and transitional state guidance to references/empty-states.md.
- Added permission and access-denied copy guidance to references/error-messages.md.
- Expanded references/verification-and-failure.md with copywork-specific verification rules.
- Added toasts, onboarding, CLI output, and navigation examples to references/examples-and-anti-patterns.md.
- Reframed the dash guidance in references/formatting-and-punctuation.md as an ASCII-hyphen
  safety warning instead of a punctuation allowance.
- Removed unicode dash naming from references/formatting-and-punctuation.md; the ASCII-hyphen
  safety warning remains.

### commit-expert

- Bumped metadata.version to 1.17.0.
- Modernized the proactive trigger reference: consistent heading naming (When to act,
  Check-in flow) and prose cleanup.
- Bumped metadata.version to 1.16.0.
- Clarified that the punctuation ban covers the em dash (U+2014) only, and added an explicit
  rule to enumerate several distinct items as Markdown bullet lists with `-` markers, never as
  a comma-separated inline run.
- Added a bulleted-body example for enumerated changes (version bumps) to examples.md.
- Bumped metadata.version to 1.15.0.
- Added a Purpose section to SKILL.md and renamed precedence headings to Priority order
  across SKILL.md and references/policy-configuration.md for a consistent skill style.
- Bumped metadata.version to 1.14.0.
- Final verification: fixed missing trailing newlines in references/commit-signing.md,
  references/host-adapters.md, and references/push-and-upstream.md.
- Bumped metadata.version to 1.13.0.
- Added references/commit-strategy.md with resolution order and strategy values: auto,
  conventional-commit, atomic-commit, focused-commit, commit-type, scope, breaking-change, and
  concern-commit.
- Expanded the commit strategy reference with three strategy dimensions (grouping, message
  format, metadata), grouping principles, weak-grouping signals, and terminology.
- Added a strategy field to the optional policy shape and wired strategy resolution into
  SKILL.md Step 2 and Step 3.
- Clarified that large commits are not banned; grouping follows logical change, not file count.
- Added an anti-pattern for adopting a commit strategy the repository or user did not ask for.
- Bumped metadata.version to 1.12.0.
- Dropped the Unicode U+2013 allowance language to keep the punctuation rule focused on the
  em dash ban, while retaining the ASCII-hyphen safety requirement for commands, flags, and
  paths.
- Added references/commit-signing.md consolidating signed-commit inspection, signing mechanics, and signature verification before push; wired into SKILL.md and referenced from policy-configuration.md, strict-mode.md, and push-and-upstream.md.
- Added a signing option to the optional policy shape.
- Modernized clean-tree checklist to git restore and added a hooks and --no-verify rule.
- Added a --no-verify bypass anti-pattern and signature verification to SKILL.md.
- Reframed the unicode-dash-in-flag example to focus on the broken command, not punctuation.

### context7-expert

- Bumped metadata.version to 1.13.0.
- Aligned the proactive trigger reference style with the other skills: consistent headings
  and comma-splice and hedging-phrase cleanup.
- Bumped metadata.version to 1.12.0.
- Added a Purpose section to SKILL.md and renamed the priority hierarchy heading to
  Priority order for a consistent skill style.

### mermaid-diagrams-expert

- Bumped metadata.version to 1.4.2.
- Modernized the proactive trigger reference: consistent headings, tightened prose, and a
  renamed inline-chart section.
- Bumped metadata.version to 1.4.1.
- Corrected the swapped rounded-rectangle and stadium flowchart shapes and documented the
  `@{ shape: <name> }` shape-definition syntax (v11.28.0+).
- Added sequence diagram features: bidirectional arrows (v11.0.0+), participant creation and
  destruction (v10.3.0+), box grouping, rect background highlighting, critical/option blocks,
  autonumber start/increment (v11.15.0+), and the "end" word parsing caveat.
- Fixed class diagram relationship syntax (Dependency `..>`, Realization `..|>` / `<|..`),
  added abstract `*` and static `$` member classifiers, capitalized the recognized annotation
  keywords, and added the namespace section plus direction and hideEmptyMembersBox tips.
- Updated misc diagrams: `xychart` keyword (legacy `xychart-beta` noted), gantt duration units
  and until dependency, gitgraph commit attributes and orientation, state note/choice/fork
  syntax, and a pie chart positive-value rule.
- Added architecture diagram sibling alignment (v11.16.0+) and the C4 dynamic and deployment
  diagram types.
- Expanded advanced-features.md with the full built-in theme list and the neo look, and noted
  that recent Mermaid versions default class and state diagrams to ELK.
- Bumped metadata.version to 1.4.0.
- Fixed the reversed identifying and non-identifying ERD relationship mapping in
  erd-diagrams.md and replaced the invalid `}{` cardinality marker with the documented
  `}|` / `|{` forms.
- Corrected the ERD key rules: only PK, FK, and UK are recognized keys, with quoted comments
  used for other constraints such as NOT NULL.
- Replaced the deprecated %%{init: ...}%% directives with the frontmatter `config:` block in
  advanced-features.md and misc-diagrams.md, and added a deprecation note.
- Replaced the empty performance flowchart with a real diagram, clarified the pinned-version
  placeholder, and rewrote the misc-diagrams.md opening in reference style instead of
  changelog style.

### redis-expert

- Bumped metadata.version to 1.4.0.
- Moved the proactive trigger guidance into references/proactive-trigger.md, aligned with the
  other skills, and rewired SKILL.md Step 0 to point at it.
- Bumped metadata.version to 1.3.0.
- Added a Purpose section to SKILL.md and renamed the anti-patterns heading to match the
  other skills.

[⬆ Back to top](#changelog)

</details>

---

## [1.9.0] - 2026-09-13

<details>
<summary>1.9.0 - 2026-09-13</summary>

### Repository

- Fixed skills.sh.json to match the skills.sh schema (groupings instead of sections) so the repository page renders with curated sections.
- Updated README install instructions to list skills and select them with --skill instead of installing every skill by default.

### context7-expert

- Bumped metadata.version to 1.11.0 in response to Snyk W011 (third-party content exposure / indirect prompt injection risk).
- Added "propose the lookup to the user, then wait" step to SKILL.md: the skill auto-loads but never auto-queries.
- Added THIRD_PARTY_CONTENT_EXPOSURE section with user consent requirements to references/security.md.
- Added "Confirm target and version with the user" section to references/selection-and-query-writing.md.
- Reworked references/proactive-trigger.md to separate activation (automatic) from transmission (always user-confirmed).
- Mode preference updated to MCP when available, CLI as fallback.

[⬆ Back to top](#changelog)

</details>

---

## [1.8.0] - 2026-09-13

<details>
<summary>1.8.0 - 2026-09-13</summary>

### commit-expert

- Bumped metadata.version to 1.11.0.
- Added conflict resolution rule to SKILL.md.
- Added atomic commit guidance to staging-and-gitignore.md.
- Added secret scanning and diff size threshold to clean-tree-checklist.md.
- Added recovery and rollback guidance to verification-and-failure.md.

### context7-expert

- Bumped metadata.version to 1.10.0.
- Added references/security.md with audited trust boundaries for remote code execution (npx), command execution, data exfiltration (query redaction), indirect prompt injection (untrusted fetched content), and persistence (skills management writes).
- Strengthened cli-mode.md with an npx execution policy requiring explicit per-request approval and version pinning after first use.
- Added "treat CLI output as untrusted data" rules to cli-mode.md.
- Added query redaction and untrusted-content handling to mcp-mode.md.
- Added trust boundaries and skills-management write controls to verification-and-failure.md.
- Referenced security.md from setup.md, cli-skills-management.md, selection-and-query-writing.md, and the SKILL.md priority hierarchy.
- Replaced repository license MIT with SSPL-1.0 (verbatim official text, copyright retained as D1ZZY4).
- Bumped metadata.version to 1.9.0.
- Added priority hierarchy to SKILL.md for conflict resolution.
- Strengthened risk classification in risk-and-budget.md with concrete high-risk examples.
- Added minimum-fetch rule to risk-and-budget.md.
- Added environment detection guidance to cli-mode.md for PowerShell, cmd.exe, and container/CI environments.
- Added explicit "do not use Context7" boundaries to SKILL.md Step 0.
- Strengthened setup.md to defer to the target agent's own documentation.
- Added package-scope disambiguation guidance to selection-and-query-writing.md.
- Clarified that Context7 confirms documentation, not user code correctness, in verification-and-failure.md.

### create-readme-expert

- Bumped metadata.version from 1.7.0 to 1.9.0.
- Fixed SKILL.md Examples section to list actual bundled example files.
- Replaced hardcoded MIT placeholder in README-1.md with generic license reference.
- Fixed typo in readme-structures.md: Prerequisiteses -> Prerequisites.

### redis-expert

- Resolved DIALECT 3 contradiction between dialect.md and search query examples.
- Removed eval-harness language and vague gold-dataset claims from command-selection.md.
- Aligned network.md command-renaming guidance with SKILL.md preference order.
- Removed hardcoded 0.9 similarity threshold default from best-practices.md.
- Redirected LangCache pointer in python-redisvl.md to this skill's semantic-cache references.
- Annotated undefined embedding/LLM placeholders in vector-query.md, hybrid-search.md, rag-pattern.md, and langcache-usage.md.
- Annotated missing collections import in command-selection.md bad example.

### copywriting-expert

- Removed self-referential phrasing from SKILL.md routing layer.

### mermaid-diagrams-expert

- Removed self-referential phrasing from SKILL.md routing layer.

[⬆ Back to top](#changelog)

</details>

---

## [1.7.0] - 2026-08-16

<details>
<summary>1.7.0 - 2026-08-16</summary>

### Added

- Step 2 in create-readme-expert now loads `references/readme-structures.md` only; `examples/README-1.md` is conditional for new README creation.
- `references/external-readme-sources.md` now includes structural-inspiration-only warning with do-not-copy rules.
- `references/anti-patterns.md` now includes a correction line for unsupported claims.
- `examples/README-missing-information.md` wording tightened from "inferred" to "documented only from".
- `examples/EXAMPLES.md` now separates reference material from the examples list.

### Changed

- Bumped create-readme-expert metadata.version to 1.7.0.
- Added workflow rules to AGENTS.md: push/commit authorization, `[Unreleased]` position rule, and changelog update guidance.

[⬆ Back to top](#changelog)

</details>

---

## [1.6.0] - 2026-08-16

<details>
<summary>1.6.0 - 2026-08-16</summary>

### Added

- Change scope control in SKILL.md to match README change size to user request.
- Missing information handling mechanism in SKILL.md.
- Audience identification section in readme-structures.md.
- Repository inspection checklist in verification-and-failure.md.
- Preserve existing README voice rules in voice-and-tone.md.
- `examples/README-unsupported-claims.md` failure case example.
- Release/update behavior in proactive-trigger.md.
- Dependency documentation rule in readme-structures.md.

### Changed

- Bumped create-readme-expert metadata.version to 1.5.0.
- Bumped context7-expert metadata.version to 1.6.0, added a risk-tiered operation
  budget in risk-and-budget.md, added traceability requirements in mcp-mode.md
  and cli-mode.md, tightened safety boundaries in setup.md for
  install/setup/auth/skills-generate, added agent-adapters.md for host adapter
  generalization, and rewrote verification-and-failure.md with concrete rules
  and hard safety boundaries.
- Narrowed proactive trigger to user-facing workflow, installation, public API, or CLI changes.
- Added placeholder warning to `examples/README-1.md`.

[⬆ Back to top](#changelog)

</details>

---

## [1.5.0] - 2026-08-16

<details>
<summary>1.5.0 - 2026-08-16</summary>

### Added

- `references/external-readme-sources.md`: moved from `examples/URL.md` as source material.

### Changed

- Bumped create-readme-expert version from 1.2.0 to 1.3.0.
- Upgraded `examples/README-library-adaptive.md`, `README-cli-adaptive.md`, and `README-missing-information.md` to evidence-based format.
- Step 4 now loads examples conditionally by project type.
- Step 0/1 repetition cleaned up in SKILL.md.
- Narrowed proactive trigger to user-facing workflow, installation, public API, or CLI changes.
- Added placeholder warning to `examples/README-1.md`.

[⬆ Back to top](#changelog)

</details>

---

## [1.4.0] - 2026-08-16

<details>
<summary>1.4.0 - 2026-08-16</summary>

### Added

- `examples/README-library-adaptive.md`: library example showing source-driven documentation.
- `examples/README-cli-adaptive.md`: CLI example showing command verification.
- `examples/README-missing-information.md`: incomplete project example showing uncertainty handling.
- Step 4 now loads all bundled README examples for structural and tonal inspiration.

### Changed

- Bumped create-readme-expert version from 1.1.0 to 1.2.0.

[⬆ Back to top](#changelog)

</details>

---

## [1.3.0] - 2026-08-16

<details>
<summary>1.3.0 - 2026-08-16</summary>

### Added

- Per-skill changelog sections with individual version tracking.
- Author and license metadata to every skill frontmatter.
- Proactive trigger references across skills.
- verification-and-failure reference across skills.
- Self-contained references across all skills.
- CHANGELOG.md with back-to-top navigation and per-skill version tables.
- SSPL-1.0 LICENSE with author D1ZZY4.
- README.md with design principles, validation instructions, and skill list.
- AGENTS.md as the canonical project rules file.

### Changed

- Improved changelog navigation with back-to-top links.
- Skill versions now reflect actual commit age rather than being uniform.
- Major version starts at 1 across all skills; minor increases by skill maturity.
- Consolidated project rules into AGENTS.md.
- Created symlinks so CLAUDE.md and replit.md both point to AGENTS.md.

### Fixed

- Removed unnecessary validation section from README.
- Removed duplicate top back-to-top link from CHANGELOG.
- Restored missing Per-skill changelog heading.
- Removed duplicate 1.3.0 entries from mermaid-diagrams-expert and redis-expert tables.

[⬆ Back to top](#changelog)

</details>

---

## [1.2.0] - 2026-08-11

<details>
<summary>1.2.0 - 2026-08-11</summary>

### Added

- Explicit skill versions in frontmatter.
- Evidence hierarchy and version-awareness to Context7 workflows.
- Renderer/version compatibility checks for Mermaid.
- Dependency-free repository validator.
- Shared verification and failure-handling guidance.
- Repository README and VERSION metadata.
- Proactive trigger references for context7-expert, commit-expert, and mermaid-diagrams-expert.

### Changed

- Tightened trigger conditions to reduce unnecessary tool usage.
- Strengthened copywriting guidance around accessibility, localization, and unsupported claims.
- Tightened Git mutation boundaries and verification language.

### Fixed

- Removed leftover TODO from copywriting anti-pattern reference.
- Added validation coverage for broken local references, duplicate names, malformed frontmatter, and forbidden em dashes.

[⬆ Back to top](#changelog)

</details>

---

## [1.1.0] - 2026-07-13

<details>
<summary>1.1.0 - 2026-07-13</summary>

### Added

- Initial release of agent-skills repository.
- context7-expert: current, version-aware library and platform documentation lookup.
- copywriting-expert: user-facing product and UI copy guidance.
- commit-expert: repository-aware Git commit and push safety.
- mermaid-diagrams-expert: maintainable Mermaid diagrams for software documentation.
- redis-expert: Redis architecture, clients, search, clustering, observability, security, and semantic caching.
- Progressive disclosure pattern: SKILL.md routing layer with references/ for detailed content.
- Validation script for frontmatter, required files, broken references, duplicate names, and forbidden em dashes.

[⬆ Back to top](#changelog)

</details>

---

## Per-skill changelog

<details>
<summary>Per-skill version tables</summary>

### Version comparison

| Version | Date | Skills | Key changes |
|---------|------|--------|-------------|
| 1.16.0 | 2026-09-29 | 7 | Plugin manifests grouped per host, commit-expert authorization model, skill structure aligned across all seven, context7-expert version separation and redacted-query consent, README compare refresh |
| 1.15.0 | 2026-09-18 | 3 | deep-research-expert auto plus 8 modes and attribution removals, mermaid and redisvl trims, README compare sync |
| 1.14.0 | 2026-09-15 | 2 | deep-research-expert review mode and quality checklist, commit-expert compare block and spec source |
| 1.13.0 | 2026-09-15 | 7 | Project Cursor marketplace, discovery keyword expansion, redis-expert 1.5.1 |
| 1.12.0 | 2026-09-15 | 7 | New deep-research-expert skill, redis-expert Iris domain and Vector Sets, mermaid-diagrams-expert new types, changelog collapsibles, plugin keyword expansion |
| 1.11.0 | 2026-09-14 | 6 | Agent marketplace manifests, skills/ move, commit-expert rename, CONTRIBUTING, agent logos, README polish, create-readme-expert diagrams reference |
| 1.10.0 | 2026-09-13 | 6 | SKILL.md Purpose sections and proactive trigger style unification, commit-expert signing and commit-strategy references, create-readme-expert W011 security response, mermaid diagram syntax corrections |
| 1.9.0 | 2026-09-13 | 6 | context7-expert W011 response, skills.sh.json schema fix, README selective install docs |
| 1.8.0 | 2026-09-13 | 6 | context7-expert security hardening, SSPL-1.0 relicensing, README install fix |
| 1.7.0 | 2026-08-16 | 1 | create-readme-expert reference loading and unsupported-claim corrections, AGENTS.md workflow rules |
| 1.6.0 | 2026-08-16 | 1 | create-readme-expert review feedback: scope control, missing info handling, audience id, inspection checklist, voice preservation, unsupported claims example |
| 1.5.0 | 2026-08-16 | 1 | create-readme-expert review fixes, evidence-based examples, version bump to 1.3.0 |
| 1.4.0 | 2026-08-16 | 1 | create-readme-expert examples additions, version bump to 1.2.0 |
| 1.3.0 | 2026-08-16 | 5 | Self-contained references, proactive triggers, verification-and-failure references, license/metadata across skills |
| 1.2.0 | 2026-08-11 | 5 | Skill versions, evidence hierarchy, proactive triggers, verification guidance |
| 1.1.0 | 2026-07-13 | 5 | Initial release, progressive disclosure pattern, validation |

### context7-expert

<details>
<summary>context7-expert version history</summary>

| Version | Date | Changes |
|---------|------|---------|
| 1.15.0 | 2026-09-29 | Separated declared, resolved, installed, indexed, and vendor current versions; redacted-query confirmation; provenance fields; per-shell CLI probes |
| 1.14.0 | 2026-09-29 | Core principles, Authorization model, and Failure handling sections aligned with the commit-expert 1.18.0 structure |
| 1.13.1 | 2026-09-15 | Node.js 18 prerequisite, ctx7 remove and MCP server URL, alias drift note, official source links |
| 1.13.0 | 2026-09-13 | Proactive trigger reference style alignment: consistent headings, comma-splice cleanup |
| 1.12.0 | 2026-09-13 | SKILL.md style unification: Purpose section, priority heading renamed to Priority order |
| 1.11.0 | 2026-09-13 | Snyk W011 response: propose lookup to the user before any query, auto-load without auto-query, MCP preferred over CLI, version options presented as choices |
| 1.10.0 | 2026-09-13 | Security audit response: trust boundaries, npx execution policy, query redaction, indirect prompt injection handling, skills management write controls; repo license moved to SSPL-1.0 |
| 1.9.0 | 2026-09-13 | Priority hierarchy for conflict resolution, concrete risk classification, environment detection, explicit do-not-use-Context7 boundaries, setup.md defers to agent documentation |
| 1.8.0 | 2026-08-16 | Priority hierarchy introduced, risk rules strengthened |
| 1.7.1 | 2026-08-16 | Metadata version bump after documentation lookup boundary work |
| 1.7.0 | 2026-08-16 | Strengthened documentation lookup boundaries |
| 1.6.0 | 2026-08-16 | Risk-tiered operation budget, traceability requirements, agent-adapters.md for host generalization, tightened setup safety boundaries, verification-and-failure rewrite |
| 1.5.0 | 2026-08-16 | Version metadata, license, self-contained references, and proactive trigger |
| 1.3.0 | 2026-08-16 | License, metadata, self-contained references, verification-and-failure reference |
| 1.2.0 | 2026-08-11 | Evidence hierarchy, version-awareness, MCP/CLI mode selection, proactive trigger |
| 1.1.0 | 2026-07-13 | Initial release |

[⬆ Back to top](#changelog)

</details>

### copywriting-expert

<details>
<summary>copywriting-expert version history</summary>

| Version | Date | Changes |
|---------|------|---------|
| 1.9.0 | 2026-09-29 | Operating modes with mutation boundaries, content versus implementation defects, empty-state state table, string non-display uses, partially verified evidence state, confidence and claims rules |
| 1.8.0 | 2026-09-29 | Core principles, Authorization model, and Failure handling sections aligned with the commit-expert 1.18.0 structure |
| 1.7.1 | 2026-09-15 | Em dash default clarifier, official language source links (KBBI, EYD, Merriam-Webster, Oxford) |
| 1.7.0 | 2026-09-13 | Proactive trigger reference modernization: consistent headings and copy cleanup |
| 1.6.0 | 2026-09-13 | SKILL.md style unification: Purpose section |
| 1.5.0 | 2026-09-13 | Anti-AI-sounding patterns, domain adaptation, codebase copy discovery, navigation/loading/permission surfaces, copywork-specific verification, expanded examples |
| 1.4.0 | 2026-09-13 | CLI output copy reference, vocabulary lookup hygiene, link and alternate text guidance, SKILL.md description expansion, broken placeholder token fix, frontmatter cleanup |
| 1.3.1 | 2026-08-16 | Reviewer fixes across references and formatting |
| 1.3.0 | 2026-08-16 | Accessibility/localization strengthening, proactive trigger, self-contained references, verification-and-failure reference |
| 1.2.0 | 2026-08-11 | Accessibility/localization strengthening, proactive trigger, self-contained references |
| 1.1.0 | 2026-07-13 | Initial release |

[⬆ Back to top](#changelog)

</details>

### commit-expert

<details>
<summary>commit-expert version history</summary>

| Version | Date | Changes |
|---------|------|---------|
| 1.18.0 | 2026-09-29 | Authorization model separating policy from permission, in-progress Git state detection, widened signature verification |
| 1.17.1 | 2026-09-15 | Conventional Commits specification source in message-style reference |
| 1.17.0 | 2026-09-13 | Proactive trigger reference style alignment: heading naming and prose cleanup |
| 1.16.0 | 2026-09-13 | Punctuation ban clarified (em dash only), bulleted-list body rule, bulleted-body example |
| 1.15.0 | 2026-09-13 | SKILL.md style unification: Purpose section, precedence headings renamed to Priority order |
| 1.14.0 | 2026-09-13 | Final verification pass: trailing-newline hygiene on three references |
| 1.13.0 | 2026-09-13 | Strategy-driven commit grouping: auto default plus seven explicit strategies, policy shape field, no mega-commit ban, resolution wired into SKILL.md steps |
| 1.12.0 | 2026-09-13 | Unicode U+2013 allowance removed, dedicated references/commit-signing.md, git restore modernization, --no-verify rule, unicode-dash flag example reframe |
| 1.10.0 | 2026-08-16 | Highest maturity tier, tightened mutation boundaries, verification language, proactive check-in flow |
| 1.3.0 | 2026-08-16 | License, metadata, self-contained references, verification-and-failure reference |
| 1.2.0 | 2026-08-11 | Evidence hierarchy, version-awareness |
| 1.1.0 | 2026-07-13 | Initial release |

[⬆ Back to top](#changelog)

</details>

### mermaid-diagrams-expert

<details>
<summary>mermaid-diagrams-expert version history</summary>

| Version | Date | Changes |
|---------|------|---------|
| 1.6.0 | 2026-09-29 | Core principles, Authorization model, and Failure handling sections aligned with the commit-expert 1.18.0 structure |
| 1.5.1 | 2026-09-18 | Trimmed generic web content from advanced-features reference |
| 1.5.0 | 2026-09-15 | New diagram types reference (venn, ishikawa, kanban, packet, radar, treemap), security reference, renderer platform matrix, v11.13.0 label fix |
| 1.4.2 | 2026-09-13 | Proactive trigger reference style alignment: consistent headings and tightened prose |
| 1.4.1 | 2026-09-13 | Modernized against Mermaid v12 docs: flowchart shape swap and @{ shape } syntax, sequence bidirectional arrows/box/rect/critical/create-destroy/autonumber, class relationship and classifier fixes plus namespaces, xychart/gantt/gitgraph/state/pie corrections, architecture align, C4 dynamic and deployment types, full theme and look lists |
| 1.4.0 | 2026-09-13 | Documented ERD cardinality and relationship-line corrections, PK/FK/UK key rules, %%{init}%% directives replaced with frontmatter config, example and wording cleanups |
| 1.3.0 | 2026-09-13 | SKILL.md style unification: Purpose section |
| 1.2.1 | 2026-08-16 | Reviewer fixes across references and formatting |
| 1.2.0 | 2026-08-11 | Renderer/version compatibility, proactive trigger, misc diagram types |
| 1.1.0 | 2026-07-13 | Initial release |

[⬆ Back to top](#changelog)

</details>

### redis-expert

<details>
<summary>redis-expert version history</summary>

| Version | Date | Changes |
|---------|------|---------|
| 1.6.0 | 2026-09-29 | Core principles, Authorization model, and Failure handling sections added, domain sections kept as the body |
| 1.5.4 | 2026-09-29 | Non-reference note repointed at `.cursor-plugin/plugin.json` after the Cursor marketplace was replaced |
| 1.5.3 | 2026-09-18 | Iris and whole-skill attribution removals, runtime rule kept |
| 1.5.2 | 2026-09-18 | Summary-level LLM primitives removal from redisvl client reference |
| 1.5.1 | 2026-09-15 | Dropped per-skill Cursor packaging pointers following the move to project-level packaging |
| 1.5.0 | 2026-09-15 | Iris agent-memory domain, native Vector Sets reference, DIALECT accuracy fix, redis.io link migration, HEXPIRE gate |
| 1.4.0 | 2026-09-13 | Proactive trigger moved to a dedicated reference file, style aligned with the other skills |
| 1.3.0 | 2026-09-13 | SKILL.md style unification: Purpose section, anti-patterns heading aligned |
| 1.2.0 | 2026-08-16 | Reviewer fixes across references and formatting |
| 1.1.0 | 2026-07-13 | Initial release |

[⬆ Back to top](#changelog)

</details>

### create-readme-expert

<details>
<summary>create-readme-expert version history</summary>

| Version | Date | Changes |
|---------|------|---------|
| 1.15.0 | 2026-09-29 | Core principles, Authorization model, and Failure handling sections aligned with the commit-expert 1.18.0 structure |
| 1.14.1 | 2026-09-15 | Verified external README URLs with checked dates, GitHub alerts docs source |
| 1.14.0 | 2026-09-14 | Diagrams reference with mermaid-diagrams-expert routing and canonical raw URL fallback |
| 1.13.0 | 2026-09-13 | Proactive trigger reference modernization: consistent headings, how-to-offer section |
| 1.12.0 | 2026-09-13 | SKILL.md structure and style unified across all skills |
| 1.11.0 | 2026-09-13 | GitHub-style alert callouts example for secrets and destructive actions, callout rules in formatting-and-punctuation, example wired into SKILL.md steps |
| 1.10.0 | 2026-09-13 | W011 response: user consent before external README fetches, security.md with untrusted content rules, anti-pattern additions |
| 1.9.0 | 2026-08-16 | Reviewer final candidate fixes |
| 1.7.0 | 2026-08-16 | Project versus skill versioning rules documented |
| 1.6.0 | 2026-08-16 | Change scope control, missing info handling, audience id, repository inspection checklist, preserve README voice, unsupported claims example, release trigger, dependency rule |
| 1.4.0 | 2026-08-16 | External README sources moved to references, Step 4 conditional loading, placeholder warning |
| 1.3.0 | 2026-08-16 | Evidence-based examples, conditional Step 4 loading, proactive trigger narrowing, placeholder warning |
| 1.2.0 | 2026-08-16 | Added adaptive README examples, Step 4 loads all bundled examples |
| 1.1.0 | 2026-07-13 | Initial release |

[⬆ Back to top](#changelog)

</details>

### deep-research-expert

<details>
<summary>deep-research-expert version history</summary>

| Version | Date | Changes |
|---------|------|---------|
| 1.6.0 | 2026-09-29 | Core principles, Authorization model, and Failure handling sections aligned with the commit-expert 1.18.0 structure |
| 1.5.2 | 2026-09-18 | Quality-gates attribution removal from quality-checklist |
| 1.5.1 | 2026-09-18 | Sources-checked block removal from code-review |
| 1.5.0 | 2026-09-18 | Auto default plus eight modes, per-mode routing, falsification and symmetry add-ons |
| 1.4.0 | 2026-09-15 | Review mode (code-review reference, routing), depth modes, critique loop, quality checklist, outline check, counterevidence and metadata footer |
| 1.0.0 | 2026-09-15 | Initial experimental release: full-scope reading, source ladder with context7-expert routing and raw URL fallback, two-source evidence grading, severity-ranked reports |

[⬆ Back to top](#changelog)

</details>

</details>
