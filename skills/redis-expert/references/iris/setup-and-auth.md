# Provision the Iris Agent Memory Store

Redis Agent Memory (RAM) is the Iris-family memory layer for AI agents, delivered as a managed service on Redis Cloud. Cloud provisions the store, the backing database, the background promotion worker, and the embedding credentials. Each store gets a store ID and a store API key used as a bearer token on every data-plane request.

## Provision and connect

1. Create the Memory service in the Redis Cloud console under Agent Memory and copy three values: server URL, store ID (32-char UUID without dashes), and store API key.
2. Export them; both official SDKs read the same convention:

```bash
export AGENT_MEMORY_BASE_URL="https://<your-service>.memory.redis.io"
export AGENT_MEMORY_STORE_ID="<your-store-id>"
export AGENT_MEMORY_API_KEY="<your-store-api-key>"
```

| Language | Package | Install |
|---|---|---|
| Python | `redis-agent-memory` | `pip install redis-agent-memory` |
| TypeScript | `@redis-iris/agent-memory` | `npm add @redis-iris/agent-memory` |

```python
import os
from redis_agent_memory import AgentMemory

with AgentMemory(
    os.environ["AGENT_MEMORY_BASE_URL"],
    store_id=os.environ["AGENT_MEMORY_STORE_ID"],
    api_key=os.environ["AGENT_MEMORY_API_KEY"],
) as agent_memory:
    print(agent_memory.health())
```

```typescript
import { AgentMemory } from "@redis-iris/agent-memory";

export const agentMemory = new AgentMemory({
  serverURL: process.env.AGENT_MEMORY_BASE_URL!,
  storeId:   process.env.AGENT_MEMORY_STORE_ID!,
  apiKey:    process.env.AGENT_MEMORY_API_KEY!,
});
```

## Auth rules

- Construct the client once per process and reuse it. The key is a bearer token scoped to one store; keep it in a secrets manager, never in source.
- The store ID is a global parameter set once on the client. Override per call only when one process talks to multiple stores.
- Do not hand-build the `Authorization` header or POST to the data-plane REST endpoints directly; that bypasses the SDK retry and error typing.
- Rotation is console-side only: regenerate the key there if one leaks. There is no short-lived-token flow.

## Sources checked

- https://github.com/redis/agent-skills (upstream `iris-development` skill, MIT; concepts followed, wording original)
- https://pypi.org/project/redis-agent-memory/
- https://www.npmjs.com/package/@redis-iris/agent-memory
- Redis Cloud console: Agent Memory service provisioning
