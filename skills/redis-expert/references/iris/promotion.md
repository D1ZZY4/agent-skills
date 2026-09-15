# Design for Async Memory Promotion

Every successful session write enqueues a promote-working-memory job, fire-and-forget. A Redis Cloud worker pool reads the session, calls an LLM to extract durable facts, and writes long-term memory. The data plane never blocks on that LLM call.

## What to assume

- **Deduplicated in 5-minute windows.** Events in the same window for one session share a key, so one promotion job runs per bucket, delayed to the window end. The window is Cloud-managed, not configurable.
- **Eventually consistent.** After a 200 write, the facts may take up to a window plus one LLM round trip to appear in search. Poll in tests; never assert synchronously.

```python
import time

def wait_for_ltm(agent_memory, *, query, owner_id, timeout_s=30.0):
    deadline = time.monotonic() + timeout_s
    while time.monotonic() < deadline:
        hits = agent_memory.search_long_term_memory(
            text=query,
            filter_={"owner_id": {"eq": owner_id}},
            limit=5,
        ).memories
        if hits:
            return hits
        time.sleep(1.0)
    raise AssertionError("promotion did not materialize in time")
```

- **Failures do not fail the write.** Submission errors are logged data-plane side while the write still returns 200; worker failures (LLM timeout, provider 429) retry in the workflow engine. A queue outage therefore delays promotion silently until Cloud monitoring catches it.
- **Idle sessions trail.** Turns that arrive after the last promotion for a quiet session wait for the next event before they are extracted.

## Sources checked

- https://github.com/redis/agent-skills (upstream `iris-development` promotion rules, MIT; concepts followed, wording original)
