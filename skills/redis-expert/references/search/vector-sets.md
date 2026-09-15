# Use Vector Sets for Native Similarity Search

Vector sets are a native Redis data type since Redis 8.0, no module required. Where an FT vector index suits large-scale filtered production search, a vector set suits moderate-scale similarity search with a simpler API: `VADD` elements with embeddings, `VSIM` to find nearest neighbours. Pick one per use case, do not maintain both for the same data.

## Basic shape

```
# Add 3-dim vectors (VALUES form takes explicit floats)
VADD points VALUES 3 0.1 0.2 0.3 item1
VADD points VALUES 3 0.4 0.5 0.6 item2

# Inspect
VDIM points          # vector dimensionality
VCARD points         # element count
TYPE points          # reports "vectorset"
VEMB points item1    # stored vector for one element

# Similar to an existing element
VSIM points ELE item1 COUNT 2 WITHSCORES

# Similar to a raw query vector
VSIM points VALUES 3 0.12 0.22 0.32 COUNT 5 WITHSCORES

# Remove
VREM points item2
```

The `FP32` form takes a binary blob instead of explicit floats and must use little-endian byte order, the same encoding rule as FT vector blobs (see [vector-query.md](vector-query.md)). Prefer `VALUES` unless payload size forces the blob form.

## Filtered search with attributes

Attach a JSON document per element, then filter inside `VSIM`:

```
VADD points VALUES 3 0.1 0.2 0.3 item1 SETATTR '{"year": 1950, "genre": "jazz"}'
VSIM points ELE item1 FILTER '.year > 1940' COUNT 5 WITHSCORES WITHATTRIBS
```

Filter expressions support numbers, quoted strings, booleans (as 1/0), arrays with `in`, and the usual comparison operators. Update attributes later with `VSETATTR key element '{...}'`.

## Quantization and build options on VADD

| Option | Effect |
|---|---|
| `Q8` (default) | Signed 8-bit quantization. Lower memory, small recall cost. |
| `BIN` | Binary quantization. Smallest footprint, lowest recall. |
| `NOQUANT` | No quantization. Highest recall, highest memory. |
| `EF n` | Build-time exploration depth (default 200). Higher improves graph quality, slows inserts. |
| `M n` | Graph links per node. Higher improves recall, costs memory. |
| `REDUCE dim` | Random projection to fewer dimensions. Only when recall budget allows. |
| `CAS` | Compare-and-set guard on updates. |

`NOQUANT`, `Q8`, and `BIN` are mutually exclusive. Per-query effort is tuned on `VSIM` with `EF`, `EPSILON` (radius bound), and `COUNT`.

## Vector set vs FT vector index

| Need | Pick |
|---|---|
| Moderate-scale similarity, simple API, no schema to manage | Vector set (`VADD` / `VSIM`) |
| Large-scale ANN with HNSW tuning (`M`, `EF_CONSTRUCTION`, `EF_RUNTIME`) | FT vector field, see [algorithm-choice.md](algorithm-choice.md) |
| Filter-narrowed KNN over TAG/NUMERIC/GEO fields | FT `=>[KNN ...]` pre-filter, see [vector-query.md](vector-query.md) |
| Blended lexical + vector ranking | `FT.HYBRID`, see [hybrid-search.md](hybrid-search.md) |
| Per-element JSON attributes with expression filters | Either; vector set `FILTER` is simpler, FT pre-filter is more expressive |

For RAG retrieval patterns built on FT indexes, see [rag-pattern.md](rag-pattern.md). Do not index the same embeddings in both a vector set and an FT index unless one is a deliberate migration staging area.

## Sources checked

- https://redis.io/docs/latest/develop/data-types/vector-sets
- https://redis.io/docs/latest/commands/vadd/ (since 8.0.0, syntax, quantization, EF)
- https://redis.io/docs/latest/commands/vsim/ (since 8.0.0, FILTER, EPSILON, EF)
- https://github.com/redis/redis/blob/unstable/modules/vector-sets/README.md (FILTER expression semantics, VSETATTR)
