# Proactive Trigger and Confirmation Flow

This file covers when to check in without waiting for an explicit commit request, and the
check-in flow to use when the working tree is dirty after real work.

## When to check in

- **You just finished a coding task** (wrote, edited, or generated files) and the working tree
  now has uncommitted changes. Before ending your turn, run `git status --short`, inspect
  ownership, and report the changes. Ask for commit approval using the flow below.
- **The user explicitly asked to commit or stage** (or a clear synonym, or named this skill
  directly). Skip the check-in entirely, go straight to Step 1 in SKILL.md. A push request also
  authorizes inspecting push state, but pushing remains a separate explicit operation covered by
  `push-and-upstream.md`.
- **You're about to end a session or declare a task done** and the tree is dirty. Check in
  before finishing, don't just leave it dirty and move on to something else.

## The check-in flow

1. Ask: "Need to commit these changes?" with three possible answers:
   - **Yes**
   - **No**
   - a **free-text custom answer** (the user might say something like "commit only the docs
     part" or "wait, let me finish first" or "yes but split it by folder")
2. Route based on the answer:
   - **No**: stop. Don't touch git. Don't ask again unless the tree changes further after
     this point.
   - **Yes**: ask one more short follow-up: does this change need any explanation from the
     user before writing the message, or is the diff self-explanatory on its own? If
     self-explanatory, skip straight to Step 1 in SKILL.md, don't make the user type anything
     else. Only ask for context when the diff genuinely doesn't explain its own why (a
     business reason, a decision between two approaches, a ticket number, something not
     visible in the code itself).
   - **Custom answer**: follow what the user actually asked for instead of the binary Yes/No
     flow. Treat it as an explicit instruction, not as a request that still needs the two
     questions above.
3. Once confirmed, proceed through the commit workflow. If ownership is unclear, a new ignored
   file is involved, or cleanup would be destructive, stop and ask a focused question instead
   of making the change.

## Why this matters

The point of this flow is to make commits feel like something the assistant naturally keeps
on top of, the way a careful developer would, not something that only happens when explicitly
summoned. But it should never feel naggy either: a clean tree means total silence, a dirty
tree after real work means one short check-in, not a running commentary.
