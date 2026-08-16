# Verification and Failure Handling

For tasks that depend on external tools, versions, renderers, repository state, or other facts
that can invalidate an otherwise plausible answer.

## Verify before using documentation

- Confirm the selected library ID, indexed version, query, and access mode before presenting an answer as Context7-backed.
- Distinguish "not checked", "checked and passed", and "checked and failed" for every claim that depends on external state.
- If a dependency or tool is unavailable, continue with a safe static workflow when possible and say so plainly.

## Failure handling

- If a Context7 call fails, times out, returns empty or clearly unhelpful results, or reports a rate limit, tell the user what happened.
- Try once more with a more specific query if the failure looks like a ranking or relevance miss rather than an outage.
- If the risk-tier budget is exhausted without a usable result, fall back to training knowledge and clearly say the answer may be outdated.

## Hard safety boundaries

- Do not initiate installation, login, logout, or credential changes during a normal documentation lookup unless the user explicitly requested it.
- Do not paste API keys into chat, shell commands, queries, or committed files.
- Do not use `npx` transient execution or any network-backed installation without explicit approval.
- Never invent successful execution, compatibility, test results, or installed tools.
- Record assumptions when they materially affect the output.
- If verification would cause a side effect, obtain the required authorization first.
