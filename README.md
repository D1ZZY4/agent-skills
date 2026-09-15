<h1 align="center">Agent Skills</h1>

<p align="center">
  <a href="https://skills.sh/D1ZZY4/agent-skills"><img src="https://skills.sh/b/D1ZZY4/agent-skills" alt="skills.sh"></a>
</p>

<p align="center">Custom expert skills, ready to use in your coding agent.</p>

<p align="center"><img src="assets/logos/amp.svg" width="40" alt="Amp" title="Amp"> <img src="assets/logos/google-g.svg" width="40" alt="Antigravity" title="Antigravity"> <img src="assets/logos/claude.svg" width="40" alt="Claude Code" title="Claude Code"> <img src="assets/logos/cline.svg" width="40" alt="Cline" title="Cline"> <img src="assets/logos/openai.svg" width="40" alt="Codex" title="Codex"> <img src="assets/logos/cursor.svg" width="40" alt="Cursor" title="Cursor"> <img src="assets/logos/gemini.svg" width="40" alt="Gemini CLI" title="Gemini CLI"> <img src="assets/logos/githubcopilot.svg" width="40" alt="GitHub Copilot" title="GitHub Copilot"> <img src="assets/logos/hermes.svg" width="40" alt="Hermes" title="Hermes"> <img src="assets/logos/opencode.svg" width="40" alt="OpenCode" title="OpenCode"> <img src="assets/logos/pi.svg" width="40" alt="Pi" title="Pi"> <img src="assets/logos/windsurf.svg" width="40" alt="Windsurf" title="Windsurf"></p>

## Install

First list the skills this repository provides:

```bash
npx skills add D1ZZY4/agent-skills --list
```

Install only the skills you want, one `--skill` flag per skill:

```bash
npx skills add D1ZZY4/agent-skills --skill context7-expert --skill commit-expert
```

Without a `--skill` flag, `npx skills add D1ZZY4/agent-skills` installs every skill at once. List first, then name only the skills you use.

### Official agent channels

Prefer your agent's own installer over the universal one above:

```bash
# Claude Code: add the marketplace, then install the plugin
/plugin marketplace add D1ZZY4/agent-skills
/plugin install agent-skills@d1zzy4-skills

# Gemini CLI: install the extension
gemini extensions install https://github.com/D1ZZY4/agent-skills

# Pi: install from git
pi install git:github.com/D1ZZY4/agent-skills

# Hermes: add the tap, then install a skill
hermes skills tap add D1ZZY4/agent-skills
hermes skills install D1ZZY4/agent-skills/context7-expert

# Cline: install from the repo
cline skill install D1ZZY4/agent-skills

# Cursor: add the marketplace, then install from chat
# marketplace file: .cursor-plugin/marketplace.json in this repo
/add-plugin agent-skills
```

Cursor, Codex, and GitHub Copilot read the `plugin.json` Agent Plugins manifest at the repo root. Antigravity, OpenCode, Windsurf, and Amp have no public marketplace. For those, use `npx skills add` above.

If your harness installs from a URL, point it at a raw skill file. Replace `<skill>` with any name from the table below:

```text
https://raw.githubusercontent.com/D1ZZY4/agent-skills/refs/heads/main/skills/<skill>/SKILL.md
```

---
## Skills

| Skill | Category | Description |
|---|---|---|
| [`context7-expert`](skills/context7-expert/SKILL.md) | Documentation | Version-aware library and platform documentation lookup; auto-loads but always proposes the query to the user before running it. |
| [`copywriting-expert`](skills/copywriting-expert/SKILL.md) | Content | User-facing product and UI copy, including buttons, errors, onboarding, accessibility text, and CLI output. |
| [`create-readme-expert`](skills/create-readme-expert/SKILL.md) | Documentation | Source-driven README creation, improvement, and audit. |
| [`mermaid-diagrams-expert`](skills/mermaid-diagrams-expert/SKILL.md) | Documentation | Maintainable Mermaid diagrams for software documentation. |
| [`commit-expert`](skills/commit-expert/SKILL.md) | Workflow | Repository-aware Git commit and push safety. |
| [`redis-expert`](skills/redis-expert/SKILL.md) | Infrastructure | Redis architecture, clients, search, clustering, observability, security, and semantic caching. |
| [`deep-research-expert`](skills/deep-research-expert/SKILL.md) | Research | Evidence-graded technical research, audits, and reviews against real sources. |

## Why these skills

Each skill defines its triggers, safety boundaries, and loading behavior in its own `SKILL.md`. Where a skill builds on an upstream original, its entry below also records how it works, why it is worth it, and how it differs. Entries are added as their comparisons are completed. Differences are tracked in [CHANGELOG.md](CHANGELOG.md).

### context7-expert

<details>
<summary>How it works, why it is worth it, and how it differs from upstream</summary>

**How it works**: the skill activates on tasks that depend on an external library, framework, SDK, or cloud service, then runs a six-step flow before answering.

1. Decides whether current documentation is needed and skips library-independent questions.
2. Picks the strongest available source: project-local docs and lockfiles first, official vendor docs second, Context7 third.
3. Chooses the available mode: the Context7 MCP when present, the `ctx7` CLI as fallback.
4. Proposes the lookup to you, including the exact library, the version, and the mode, and waits for your confirmation before any query is sent.
5. Resolves the library precisely from your manifests, fetches only the reference the task needs, and applies it without silently upgrading your dependency version.
6. Reports what was verified and what stays uncertain instead of fabricating a method, option, version, or compatibility claim.

**Why it is worth it**: model training data goes stale, and answers based on "latest" break projects pinned to older versions. This skill answers from current, version-matched documentation. Because every lookup requires approval first, there are no surprise token costs, no project details sent to a remote service without explicit consent, and no invented installation states.

**What differs from the official**: the official Context7 setup ships as three separate skills in `upstash/context7` (`find-docs` for the CLI lookup flow, `context7-mcp` for the MCP flow, and `context7-cli` for full CLI coverage) plus two standalone rules files (`rules/context7-cli.md` and `rules/context7-mcp.md`). This repo replaces all five files with a single installable skill. In the table, &check; means the version covers it, &cross; means it is absent or not specified, and &bull; means it is partial or varies.

| Category | Official `upstash/context7` | This repo `context7-expert` |
|----------|----------------------------|-----------------------------|
| Packaging | &bull; 3 skills + 2 rules files; lookup mode follows the file you install (`find-docs` = CLI, `context7-mcp` = MCP) | &check; 1 skill, chooses its own mode |
| Consent before any lookup | &cross; queries run as soon as the need appears | &check; proposes query, version, and mode, then waits |
| Source priority | &bull; Context7 over web search | &bull; evidence ladder: project-local &rarr; vendor docs &rarr; Context7 |
| Version handling | &bull; optional `/org/project/version` IDs | &check; checks lockfiles and manifests, never silently swaps major versions |
| Query discipline | &bull; one concept per query, max 3 commands | &check; same rules plus budget tiers in one reference |
| Quota and auth handling | &bull; tells the user and suggests login | &check; same, plus falls back only with flagged uncertainty |
| Security and trust boundary | &bull; warns not to put secrets in queries | &check; treats fetched docs as untrusted data (W011), query redaction, npx execution policy |
| Uncertainty reporting | &cross; only for quota errors | &check; explicit verified-versus-uncertain report per lookup |
| Documentation and structure | &bull; flat, single-purpose SKILL.md bodies | &check; 10 references, loaded only for the current step |
| License | &bull; MIT licensed (see upstream LICENSE) | &check; unified SSPL-1.0 |

**Strengths**: version-accurate answers; consent-based privacy and cost control; precise, narrow fetches; a documented fallback ladder; security rules for untrusted fetched content; honest uncertainty reporting.

**Weaknesses**: every lookup needs your confirmation, which adds friction for fast, fully-autonomous workflows; it needs the MCP or the `ctx7` CLI to reach Context7 (without them it degrades to local docs and flagged uncertainty); coverage depends on the Context7 index, so new or niche libraries can be missing; and it ships ten references, so the install is larger than a single SKILL.md (progressive disclosure keeps the loaded part small).

**Proactive loading**: no invocation phrase is required. The skill auto-loads whenever the task matches a trigger, for example, a named dependency plus an API question, a version number, migration work, setup, or an error from a specific library. This matters most on models that default to answering from memory: the skill directs the agent to check current documentation instead. Auto-loading never means auto-querying. The consent gate still applies before any lookup is sent.

**Sources**: [upstash/context7](https://github.com/upstash/context7) (MIT) with its [find-docs](https://github.com/upstash/context7/tree/master/skills/find-docs), [context7-mcp](https://github.com/upstash/context7/tree/master/skills/context7-mcp), and [context7-cli](https://github.com/upstash/context7/tree/master/skills/context7-cli) skills plus [rules files](https://github.com/upstash/context7/tree/master/rules); [context7.com](https://context7.com) for API keys and rate limits.

</details>

### deep-research-expert

<details>
<summary>How it works, why it is worth it, and how it differs from upstream</summary>

**How it works**: the skill proposes a research plan (scope, sources, stopping rule), reads the full scope before judging any of it, climbs a six-rung source ladder, grades each load-bearing claim with evidence labels, and delivers a severity-ranked report. For code review it switches to a dedicated two-axis flow (Standards vs Spec) against a caller-supplied fixed point.

**Why it is worth it**: audits fail in predictable ways (sampled files presented as full coverage, one snippet treated as confirmation, invented links). This skill turns each failure into a named rule with a check, so the report states what was verified, what was partial, and what was never checked.

**What differs from the originals**: there are two upstreams. [mattpocock/skills code-review](https://raw.githubusercontent.com/mattpocock/skills/refs/heads/main/skills/engineering/code-review/SKILL.md) is a single-purpose diff reviewer (two axes, parallel sub-agents, Fowler smell baseline). [199-biotechnologies/claude-deep-research-skill](https://github.com/199-biotechnologies/claude-deep-research-skill) (MIT) is a phased research pipeline with depth modes, disk-persisted evidence stores, and validation scripts. This repo generalizes the first beyond diffs (any technical surface, plus source ladder and grading) and keeps the second lean (no file outputs, scripts, or HTML reports by default; evidence labels instead of JSONL stores). Wording is original throughout. In the table, &check; means the version covers it, &cross; means it is absent or not specified, and &bull; means it is partial or varies.

| Category | mattpocock `code-review` | `199-biotechnologies` deep-research | This repo `deep-research-expert` |
|----------|--------------------------|-------------------------------------|----------------------------------|
| Scope | &bull; diffs since a fixed point only | &check; any research question | &check; any technical surface, plus a dedicated review mode |
| Depth control | &cross; one fixed flow | &check; quick/standard/deep/ultradeep modes | &bull; plan proposal with stopping rule, one critique loop max |
| Source hierarchy | &cross; repo docs assumed | &bull; multi-provider search, no fixed ladder | &check; six-rung ladder, weaker never overrules stronger |
| Claim verification | &bull; spec-line quotes per finding | &check; 3+ sources per claim, validation scripts | &check; two-source rule plus Verified/Partial/Unverified labels |
| Evidence persistence | &cross; report only | &check; JSONL stores, HTML/PDF outputs | &cross; report carries methodology instead |
| Code review mode | &check; Standards vs Spec axes | &cross; | &check; adapted axes plus smell baseline |
| License | &bull; see upstream repo | &bull; MIT licensed | &check; unified SSPL-1.0 |

**Strengths**: full-scope reading before judging; explicit uncertainty labels; raw URL fallbacks so missing skills degrade gracefully instead of guessing; a review mode with independent axes that stop one verdict from masking the other.

**Weaknesses**: thorough by design, so slower than a spot check; needs network access for the fetch-and-verify steps (without it, it degrades to labeled uncertainty rather than answers); no executable validators, so citation hygiene relies on agent discipline rather than scripts.

**Proactive loading**: offers research when accuracy, currency, or completeness is questioned, when a claim carries version/URL/syntax risk, or before material ships as authoritative. Stays quiet for small stable questions answerable from verified local material.

**Sources**: [mattpocock/skills code-review](https://raw.githubusercontent.com/mattpocock/skills/refs/heads/main/skills/engineering/code-review/SKILL.md); [199-biotechnologies/claude-deep-research-skill](https://github.com/199-biotechnologies/claude-deep-research-skill) ([SKILL.md](https://raw.githubusercontent.com/199-biotechnologies/claude-deep-research-skill/main/SKILL.md), MIT). Later additions adapt its quality gates (as a checklist), outline refinement, and counterevidence discipline the same way.

</details>

### commit-expert

<details>
<summary>How it works, why it is worth it, and how it differs from upstream</summary>

**How it works**: the skill inspects repository policy, working-tree state, diffs, hooks, branch/upstream configuration, and commit conventions before any mutation, then stages explicit paths, writes the message per repository convention, verifies checks, and mutates only within the granted scope. A dirty tree after real work triggers one short check-in, never silent commits.

**Why it is worth it**: commits stay reviewable, revertible, signed, and secret-free without relying on agent goodwill. The safety boundary (inspection free, mutation needs explicit authorization) makes the most dangerous Git operations boring and predictable.

**What differs from the originals**: there are two upstreams. [awesome-copilot conventional-commit](https://raw.githubusercontent.com/github/awesome-copilot/main/skills/conventional-commit/SKILL.md) is a 72-line XML prompt template for message format only, and it auto-runs `git commit` with no confirmation step. [caveman-commit](https://raw.githubusercontent.com/JuliusBrussee/caveman/main/skills/caveman-commit/SKILL.md) (106k stars) writes terse Conventional Commits messages with strict subject/body rules and explicit message-only boundaries. This repo keeps caveman-grade message discipline and adds the full safety workflow neither upstream has. In the table, &check; means the version covers it, &cross; means it is absent or not specified, and &bull; means it is partial or varies.

| Category | awesome-copilot `conventional-commit` | `caveman-commit` | This repo `commit-expert` |
|----------|---------------------------------------|------------------|---------------------------|
| Scope | &bull; message format only | &bull; message text only | &check; full workflow: inspect, stage, message, verify, push |
| Confirmation before mutating | &cross; commits with no confirmation | &check; never stages or commits at all | &check; explicit authorization per side effect |
| Message format | &check; Conventional Commits XML template | &check; terse rules, 50/72 chars, never-include list | &check; same discipline, repo convention wins over template |
| Commit strategy | &cross; | &cross; | &check; auto plus explicit grouping strategies |
| Signing | &cross; | &cross; | &check; GPG inspection, mechanics, pre-push verification |
| Push and upstream | &cross; | &cross; | &check; authorization, upstream checks, no force-push |
| Proactive check-in | &cross; | &cross; | &check; one short prompt on a dirty tree after real work |
| License | &bull; see upstream repo | &bull; see upstream repo | &check; unified SSPL-1.0 |

**Strengths**: message quality on par with the best message-only skills; plus signed commits, secret scanning, strategy-driven grouping, and push safety they do not attempt; the check-in flow keeps trees from rotting silently.

**Weaknesses**: heavier than a message-only skill: policy inspection, diff review, and explicit confirmations add steps to every commit; needs a configured signing key and upstream to use the full flow; overkill for a trivial single-file typo fix where `caveman-commit` style output alone would do.

**Proactive loading**: checks in once when real work left the tree dirty, and stays silent on a clean tree. Never stages, commits, or pushes to earn that diligence.

**Sources**: [awesome-copilot conventional-commit](https://raw.githubusercontent.com/github/awesome-copilot/main/skills/conventional-commit/SKILL.md); [caveman-commit](https://raw.githubusercontent.com/JuliusBrussee/caveman/main/skills/caveman-commit/SKILL.md); [Conventional Commits specification](https://www.conventionalcommits.org/en/v1.0.0/#specification).

</details>

---
## Setup

Each skill works once its directory is inside a skills path your agent reads. The standard shape is a `SKILL.md` routing file plus optional `references/` with detailed procedures.

Preferred path: install with `npx skills add` as shown above.

Manual path: copy or symlink the skill directory into a skills path your agent reads, then confirm the agent lists the skill. Each skill documents its own triggers and safety rules in its `SKILL.md`.

## Contributing

Want to fix a skill or propose a new one? Start with [CONTRIBUTING.md](CONTRIBUTING.md).

## License

SSPL-1.0. Copyright (c) 2026 D1ZZY4. See [LICENSE](LICENSE).
