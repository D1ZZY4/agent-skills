---
name: redis-expert
description: >
  All-in-one Redis expertise covering data modeling and key naming, client connections
  (pooling, pipelining, client-side caching, timeouts), clustering and replication, Redis
  Search (FT.CREATE, vector and hybrid search, RAG pipelines), observability and incident
  triage, production security hardening, semantic caching for LLM responses via
  LangCache, and agent memory via Redis Iris (session events, long-term memory,
  background promotion). Use whenever designing, writing, reviewing, or debugging anything that touches
  Redis: choosing a data structure, naming keys, configuring a client, sharding across a
  cluster, building or tuning a search index, monitoring or diagnosing performance, hardening
  a deployment, caching LLM completions, or wiring persistent memory for an AI agent, merged
  into one skill so the right domain loads automatically without picking between separate ones.
license: SSPL-1.0
metadata:
  version: 1.6.0
  author: D1ZZY4
  priority: low
---

# Redis Expert

## Purpose

Provide all-in-one Redis expertise across eight domains: data modeling and key naming,
client connections, clustering and replication, Redis Search, observability, security,
semantic caching, and agent memory. Reach for this skill any time code, config, or a design decision touches
Redis. Details live in `references/<domain>/`; load the file for the domain and topic in
question rather than guessing. Retained technical guidance follows the upstream material
where available, with qualifiers where the aggregate must distinguish Redis versions,
modules, clients, or deployment models.

## Core principles

1. Reach for this skill whenever code, config, or a design decision touches Redis, not only when the user names it.
2. Pick the data structure from the access pattern, not the data's shape.
3. Load every domain the task touches. A production search deployment spans core, search, security, and observability at once.
4. Validate Redis-specific guidance against the target version, modules, client library, and deployment model. General database intuition leads in the wrong direction often enough to be unreliable here.
5. Qualify version-dependent behavior explicitly, since a dimension mismatch may be rejected while a metric mismatch only degrades relevance silently.
6. Prefer the incremental `SCAN` family and pooled connections over shortcuts that only work at small scale.
7. Prefer per-application ACLs with least privilege over one shared credential.
8. No em dashes in generated guidance.

## Authorization model

Redis work is mostly advisory. Authorization matters for the operations that reach a live system:

| User instruction | Authorized scope |
| --- | --- |
| "which data structure" | Reasoning and recommendation, no connection required |
| "how do I index this" | Schema and query design, no index is created |
| "this is slow" | Diagnosis from metrics, SLOWLOG, and FT.PROFILE output you provide |
| "apply this config" | The configuration change as a proposal, applied only when asked to apply it |
| "connect to production" | A separate authorization naming the target; report the risk before connecting |
| "flush the cache" | Explicit and specific. Never a step toward another task. |

Never connect to a live deployment, run a destructive command, or change security settings as a
convenience step toward answering a question.

## Step 0: Trigger proactively

Reach for this skill any time code, config, or a design decision touches Redis, not only when
the user says the word "Redis". Read `references/proactive-trigger.md` for the full trigger
list, the confidence rule, and when to stay quiet.

## Step 1: Route to the right domain

| Working on | Domain | Reference folder |
|---|---|---|
| Picking a data structure, naming keys, modeling an entity | Core | `references/core/` |
| Configuring a client, pooling, pipelining, timeouts, client-side caching, avoiding slow commands | Connections | `references/connections/` |
| Sharding, hash tags, CROSSSLOT errors, read replicas | Clustering | `references/clustering/` |
| Search index design, FT.SEARCH/FT.AGGREGATE/FT.HYBRID, vector search, RAG | Search | `references/search/` |
| Metrics, SLOWLOG, INFO, incident triage, Redis Insight | Observability | `references/observability/` |
| Auth, ACLs, TLS, network exposure, hardening for production | Security | `references/security/` |
| Semantic caching of LLM responses with LangCache | Semantic cache | `references/semantic-cache/` |
| Agent session events, long-term memory, background promotion with Iris | Agent memory | `references/iris/` |

More than one domain is often relevant to a single task (a production search deployment
touches core, search, security, and observability at once), load each relevant domain file
rather than picking only one.

## Core: data modeling and key naming

Pick the Redis type that matches the *access pattern*, not just the data's shape: String for
atomic counters, Hash for objects with independently-updated fields, List for queues, Set for
membership checks, Sorted Set for rankings, JSON for nested data, Stream for event logs,
Vector Set for similarity search. The classic anti-pattern is stuffing a flat object into a
serialized string, forcing fetch-parse-mutate-rewrite for every field update, use a Hash
instead.

Key names: lowercase, colon-separated, stable hierarchy (`user:1001:profile`), short but
readable, prefixed per tenant when multi-tenant (`tenant:42:user:7:cart`).

See `references/core/choose-data-structure.md` and `references/core/key-naming.md`.

## Connections: talking to Redis efficiently

Pool or multiplex, never open a new connection per request, that's the single biggest client
mistake. Pipeline independent commands into one round trip. Never call whole-keyspace-scanning
commands (`KEYS`, `SMEMBERS` on a large set, `HGETALL` on a large hash) in production, use the
incremental `SCAN`/`SSCAN`/`HSCAN` variants instead. Enable RESP3 client-side caching for
hot, rarely-written keys. Set explicit connect and read timeouts matched to the application's
actual failure model, don't rely on client defaults.

See `references/connections/` (pooling, pipelining, blocking, client-cache, timeouts).

## Clustering: sharding and replication

Redis Cluster hashes each key to one of 16,384 slots. Any multi-key command (`MGET`, `SDIFF`,
transactions, pipelines, multi-key Lua) needs all its keys on the same slot, or it fails with
`CROSSSLOT`. Hash tags (the part between `{` and `}`) force co-location, scope the tag to the
meaningful entity (`{user:1001}`), don't over-tag since that creates hotspots. For read-heavy
workloads, route reads to replicas, but replicas are eventually consistent, never read your
own writes from one and never use replica reads for anything requiring strict freshness.

See `references/clustering/hash-tags.md` and `references/clustering/read-replicas.md`.

## Search: indexing, querying, vectors, and RAG

Three query commands: `FT.SEARCH` for direct document retrieval (the default choice),
`FT.AGGREGATE` for faceting and analytics pipelines, `FT.HYBRID` (Redis 8.4+) for blending
lexical (BM25) and vector similarity in one fused query. `FT.CREATE` always needs an explicit
`PREFIX` and should use `DIALECT 2`. Pick the narrowest field type for the access pattern,
`TAG` for exact-match filtering is roughly 10x faster than misusing `TEXT` for it. For vector
fields, `DIM` must match the embedding model and the distance metric must match the retrieval
design. Depending on the Redis, module, and client versions, a dimension mismatch may be rejected
at index or query time, while a metric or model mismatch can degrade relevance without an obvious
application error. `HNSW` for production-scale approximate search,
`FLAT` for small exact-match corpora. Zero-downtime schema changes go through index aliases,
never repoint application queries at a raw index name directly.

See `references/search/` for the full breakdown: schema and field types, query syntax,
aggregation and cursors, vector and hybrid search, native vector sets, RAG patterns, index management, debugging
with `FT.EXPLAIN`/`FT.PROFILE`, and per-client examples (`references/search/clients/`) for
redis-py, Jedis, and RedisVL.

## Observability: monitoring and incident triage

Export `used_memory`, `connected_clients`, `blocked_clients`,
`instantaneous_ops_per_sec`, `keyspace_hits`/`keyspace_misses` (hit ratio), and
`rejected_connections` from `INFO` to the monitoring system. For ad-hoc diagnosis:
`SLOWLOG GET` to find operations that exceeded the slow-command threshold, `MEMORY DOCTOR`
for a plain-language summary of memory pressure, `CLIENT LIST` for connection state,
`FT.PROFILE` for slow search queries. Redis Insight is the official GUI for interactive
exploration, not a replacement for exported metrics.

See `references/observability/metrics.md` and `references/observability/commands.md`.

## Security: production hardening

For production deployments, authenticate and use TLS according to the managed service or
self-hosted topology. A production Redis with no authentication is a common breach pattern.
Prefer per-application ACL users with the minimum commands and key patterns they actually need
over one shared `requirepass`, so a leaked credential has a bounded blast radius. Restrict
network exposure with `bind`, `protected-mode yes`, and firewall rules limiting access to
application subnets. `bind 0.0.0.0` with `protected-mode no` exposes Redis to the entire network.
Prefer ACL restrictions and network controls for destructive commands (`FLUSHALL`, `DEBUG`,
`CONFIG`). If command renaming or disabling is also used, verify client and operational tooling
compatibility because it can break expected command names.

See `references/security/auth.md`, `references/security/acls.md`, and
`references/security/network.md`.

## Semantic cache: caching LLM responses with LangCache

Cache-aside pattern in front of any LLM call: search the cache by prompt similarity first, on
a hit return the stored response, on a miss call the LLM and store the result. Similarity
thresholds are workload and embedding-model heuristics, not portable defaults. Start
conservatively, then calibrate them against an evaluation set while considering privacy, tenant
isolation, TTL, invalidation, and poisoning risk.
Never share one cache across unrelated task types (a code question and a password-reset
question are semantically distinct even if the format is similar), use separate cache IDs or
attribute-based filtering per task.

See `references/semantic-cache/langcache-usage.md` and
`references/semantic-cache/best-practices.md`. LangCache is currently in preview on Redis
Cloud, behavior may change.

## Agent memory: session and long-term memory with Iris

Two tiers served by the managed Redis Agent Memory data plane: append-only session events per conversation (cheap, ordered, no LLM on the write path) and semantically searchable long-term memory with a default 1-year TTL. A background promotion worker extracts durable facts from sessions on a 5-minute deduplication window, so long-term memory is eventually consistent after each write.

Append every turn with one stable `session_id` and a tz-aware UTC timestamp; scope long-term records with `owner_id`, `namespace`, `topics`, and `memory_type` at write time; search server-side with structured filters plus a similarity threshold instead of filtering client-side.

See `references/iris/setup-and-auth.md`, `references/iris/session-memory.md`,
`references/iris/long-term-memory.md`, and `references/iris/promotion.md`.

## Failure handling

When Redis guidance depends on a fact that could not be confirmed:

1. state the version, module, or client assumption the guidance rests on
2. distinguish a hard rejection from a silent degradation, since the second is the more dangerous case
3. do not present a best practice as portable when it is workload- or version-specific
4. say when the right answer is to measure, for example a similarity threshold that must be calibrated
5. never connect to, reconfigure, or flush a live deployment to resolve your own uncertainty

A wrong similarity threshold degrades quietly. An unverified claim about one does too.

## Anti-patterns

- Storing a flat, independently-updated object as a serialized string instead of a Hash
- Using `TEXT` for a field that needs exact-match filtering instead of `TAG`
- Calling `KEYS`, unbounded `SMEMBERS`, or unbounded `HGETALL` against production data instead
  of the incremental `SCAN` family
- Opening a new connection per request instead of pooling or multiplexing
- Multi-key operations in a clustered deployment without hash tags to co-locate the keys
- Reading from a replica for anything requiring strict freshness (balances, idempotency state)
- A `VECTOR` field whose `DIM` or `DISTANCE_METRIC` doesn't match the actual embedding model
- Production Redis with no password, no TLS, or bound to `0.0.0.0` with protected mode off
- One shared semantic cache spanning unrelated task types
- Using long-term memory as the conversation buffer instead of session events
- Assuming promoted memories are searchable synchronously after a session write
- Guessing at a Redis-specific best practice from general database intuition instead of
  checking the relevant reference, Redis has enough specific behavior (CROSSSLOT, silent
  vector dimension mismatches, RESP3 requirements) that intuition from other databases
  frequently leads in the wrong direction

## Bundled references

Organized by domain, matching the upstream official skills plus the Iris agent-memory domain:

- `references/proactive-trigger.md`: when to reach for this skill without being asked, and the
  confidence rule.
- `references/core/`: choosing a data structure, key naming conventions.
- `references/connections/`: pooling, pipelining, blocking commands, client-side caching,
  timeouts.
- `references/clustering/`: hash tags, read replicas.
- `references/search/`: schema and field types, query syntax and optimization, aggregation
  and cursors, vector and hybrid search, native vector sets, RAG patterns, dialect, index management and
  debugging, and per-client examples in `references/search/clients/`.
- `references/observability/`: metrics to monitor, built-in debugging commands.
- `references/security/`: authentication and TLS, ACLs, network restriction.
- `references/semantic-cache/`: LangCache usage and tuning best practices.
- `references/iris/`: Agent Memory store setup and auth, session memory, long-term memory, background promotion.

## Non-reference bundled content

- No evaluation suite is bundled in this aggregate. Validate Redis-specific guidance against the
  target Redis version, modules, client library, and deployment model before treating it as an
  authoritative implementation contract.
- Cursor plugin packaging lives at the project level (`.cursor-plugin/plugin.json`),
  covering every skill in this repository rather than this skill alone.

The target Redis version and deployment documentation remain the authority for runtime behavior.
