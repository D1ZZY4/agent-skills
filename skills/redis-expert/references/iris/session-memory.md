# Record and Read Session Memory

Session memory is the append-only, ordered conversation history for one session: cheap writes, no LLM cost on the write path, scoped by the store TTL. Long-term memory is the extracted, searchable counterpart; see [long-term-memory.md](long-term-memory.md) for when each tier applies.

## Tier rule

Append every turn as a session event and let background promotion decide what becomes durable (see [promotion.md](promotion.md)). Write to long-term memory directly only when the fact is already structured and extraction would add nothing. Never use long-term memory as the conversation buffer: it is vector-indexed per write and unordered, so turns lose order and every turn pays embedding cost.

## Append correctly

Carry one `session_id` for the whole conversation. The session is created on first write; omitting the ID mints a new session per turn and starves promotion of context. Always pass a tz-aware UTC timestamp in Python (`datetime.now(timezone.utc)`), a `Date` in TypeScript.

```python
from datetime import datetime, timezone
from redis_agent_memory import AgentMemory, models

agent_memory.add_session_event(
    session_id="chat-2026-05-18-42",
    actor_id="user-42",                    # who said it: user, agent, or system id
    role=models.MessageRole.USER,          # USER | ASSISTANT | SYSTEM
    content=[{"text": user_msg}],          # typed parts; text only today
    created_at=datetime.now(timezone.utc),
    metadata={"channel": "web"},           # optional JSON, 16 KB max
)
```

Constraints: IDs (`store_id`, `session_id`, `actor_id`) are 1-64 chars of `[a-zA-Z0-9-]`; `metadata` is capped at 16 KB. Keep the returned `event_id` if later deletion is possible. Each new event refreshes the session TTL.

## Read with the narrowest call

| Call | Returns | Use for |
|---|---|---|
| `get_session_memory` | All events in `created_at` order plus `owner_id` | Rebuilding prompt context |
| `get_session_event` | One event by ID (O(1)) | Targeted fetch or delete prep |
| `list_sessions` | Paged session IDs (limit default 100, max 1000) | Admin and debug listing |

The session `owner_id` comes from the first event's `actor_id` and never changes. Each event carries two timestamps: client-supplied `created_at` (ordering, agent truth) and server-set `system_timestamp` (ingestion time, diagnostics for clock skew or replays). Pass page tokens back verbatim.

Deleting a session or event does not remove already-promoted long-term memories; delete those separately.

## Sources checked

- https://github.com/redis/agent-skills (upstream `iris-development` session rules, MIT; concepts followed, wording original)
