# Proactive Trigger

When to reach for this skill without waiting for the user to name Redis, and when to stay quiet.

## When to act

Reach for this skill any time code, config, or a design decision touches Redis at all:

- writing a Redis client call
- designing a schema or key structure
- setting up a search index
- reviewing a PR that adds Redis usage
- debugging a slow or failing Redis operation
- hardening a deployment before production

## Confidence rule

If you are genuinely uncertain whether a design choice is optimal, for example a data structure
pick, a field type, or a timeout value, check the relevant reference rather than guessing from
general database intuition. Redis has specific, sometimes counterintuitive right answers; see
the anti-patterns list in SKILL.md for common wrong intuitions.

## When to stay quiet

- The question covers a general programming or database concept that applies to every store,
  and no Redis-specific answer is in question.
- The user explicitly asked to skip Redis references or tooling.