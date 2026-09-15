# Write, Search, and Organize Long-Term Memory

Long-term memory holds extracted facts, episodes, and retained messages, searchable semantically across sessions. Default TTL is 1 year unless the store overrides it. Every pattern below composes with session memory in [session-memory.md](session-memory.md) and the async promotion in [promotion.md](promotion.md).

## Bulk create with deterministic IDs

One call carries 1-100 records. Supply a stable ID per logical fact so retries never duplicate. The response splits into `created` IDs and per-ID `errors`; always inspect `errors` and retry only the failed IDs, never the whole batch.

```python
from redis_agent_memory import AgentMemory, models

res = agent_memory.bulk_create_long_term_memories(memories=[{
    "id":          "user-42-pref-theme",     # deterministic: same fact, same id
    "text":        "User 42 prefers dark mode.",   # 1-50000 chars
    "memory_type": models.MemoryType.SEMANTIC,     # semantic | episodic | message
    "owner_id":    "user-42",
    "namespace":   "preferences",
    "topics":      ["ui", "theme"],          # up to 50 tags, 1-100 chars each
}])
failed = {e.id for e in res.errors or []}
```

One call per fact burns a round trip and an embedding call each; random IDs per retry create duplicates. Update text or tags later with `update_long_term_memory` rather than re-creating.

## Search server-side, never client-side

Combine structured filters with semantic ranking in one call. Filters run before ranking; pulling 100 records to filter locally wastes the vector work and can miss the record past the cap.

```python
res = agent_memory.search_long_term_memory(
    text="dashboard theme preference",
    similarity_threshold=0.7,                # normalized cosine 0-1; start 0.7, tune per workload
    filter_op=models.FilterConjunction.ALL,  # AND across filter keys ("any" for OR)
    filter_={"owner_id": {"eq": "user-42"}}, # trailing underscore: filter is reserved
    limit=5,                                 # 1-100
)
```

Filter operators: `eq`, `ne`, `in`, `all` on `session_id`, `owner_id`, `namespace`, `topics`, `memory_type`; `gt`, `lt`, `gte`, `lte`, `eq` on `created_at` with tz-aware datetimes. Omit `text` for filter-only browsing. Page with the opaque `next_page_token`, verbatim.

## Organize at write time

| Field | Purpose |
|---|---|
| `owner_id` | Who the memory is about. Always set for per-user facts; searches without it read across tenants. |
| `namespace` | Logical bucket: `preferences` vs `interactions` vs `tools`. |
| `topics` | Categorical tags for cheap scoping. |
| `memory_type` | `semantic` (durable fact), `episodic` (dated event), `message` (verbatim turn). |

Keep structure in fields, not in prose: a fact like `[owner=user-42] prefers dark mode` inside `text` cannot be filtered without an LLM re-parse. Clearing a field on update takes an empty string; omitting it leaves the value unchanged.

## Sources checked

- https://github.com/redis/agent-skills (upstream `iris-development` LTM rules, MIT; concepts followed, wording original)
