# Use DIALECT 2 for Query Syntax

Pass `DIALECT 2` on every `FT.SEARCH` / `FT.AGGREGATE` / `FT.HYBRID` call. Dialects 1, 3, and 4 are deprecated in Redis 8, but `DIALECT 1` remains the server default, so omitting the dialect silently changes parsing. Vector query attributes (the `=>[KNN ...]` form) require DIALECT 2 to parse.

**Exception for GEOSHAPE:** `DIALECT 3` is still required for `GEOSHAPE WITHIN` / `CONTAINS` predicates (deprecated but functional; `DIALECT 1` remains the default on both Redis 7.x module and Redis 8 deployments). Pass the dialect explicitly per query instead of relying on the server default.

**Correct:** Specify DIALECT 2 explicitly on every call.

```
# In raw commands, specify DIALECT 2 at the end
FT.SEARCH idx:bicycle "@model:hyperion" DIALECT 2

FT.AGGREGATE idx:bicycle "@type:{mountain}"
    GROUPBY 1 @brand
    REDUCE COUNT 0 AS bike_count
    DIALECT 2
```

**Note on Redis 8 and DIALECT:** Dialects 1, 3, and 4 are deprecated but still accepted, and the server default remains `DIALECT 1` (changeable via `FT.CONFIG SET DEFAULT_DIALECT`). Neither redis-py nor Jedis sets a dialect on your behalf. Always pass `DIALECT 2` explicitly so behavior is identical across Redis versions and clients.

**Why DIALECT 2:**

- Required for vector search (`=>[KNN ...]` attribute syntax).
- Required for `PARAMS` placeholder binding.
- Predictable handling of special characters and NULL-like missing fields.
- The dialect new search features target; deprecated dialects stay for compatibility only.

**Incorrect:** Relying on the server-side default with a client library that pins an older dialect.

```
# Bad: omitting DIALECT in a vector query with a legacy redis-py, falls back to DIALECT 1 and rejects =>[KNN ...]
FT.SEARCH idx:bicycle "*=>[KNN 10 @embedding $vec AS score]" PARAMS 2 vec "..."
```

## Client mirrors

```python
# redis-py, STEP_START dialect
# Mirrors doctests/search_quickstart.py
from redis import Redis
r = Redis()
# Modern redis-py does not set DIALECT; set explicitly on every query
r.ft("idx:bicycle").search("@model:hyperion", dialect=2)
# STEP_END
```

```java
// Jedis, STEP_START dialect
// Mirrors SearchQuickstartExample.java
import redis.clients.jedis.UnifiedJedis;
import redis.clients.jedis.search.FTSearchParams;
import redis.clients.jedis.search.SearchResult;

try (UnifiedJedis jedis = new UnifiedJedis("redis://localhost:6379")) {
    SearchResult res = jedis.ftSearch("idx:bicycle",
        "@model:hyperion",
        FTSearchParams.searchParams().dialect(2));
}
// STEP_END
```

## Upstream sources

- redis-py: [`doctests/search_quickstart.py`](https://github.com/redis/redis-py/blob/master/doctests/search_quickstart.py)
- Jedis: [`SearchQuickstartExample.java`](https://github.com/redis/jedis/blob/master/src/test/java/io/redis/examples/SearchQuickstartExample.java)
- Reference: [Query Dialects](https://redis.io/docs/latest/develop/ai/search-and-query/advanced-concepts/dialects/)

## Sources checked

- https://redis.io/docs/latest/develop/ai/search-and-query/advanced-concepts/dialects/ (deprecated status, DIALECT 1 still default)
