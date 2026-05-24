# @clawie-dev/sdk

Planned TypeScript SDK for the Clawie REST + WebSocket API
([spec 023](https://github.com/clawie-dev/specs/tree/main/speckit/023-rest-api)).
Auto-generated from the OpenAPI spec, with typed handlers for every endpoint
and topic-filtered WebSocket subscriptions.

> **Status:** Pending. The package is not yet published to npm. The repo
> currently holds only the README and LICENSE; bootstrap lands in a v1.x
> release. Today, consume the Clawie REST API directly — its surface is
> small enough that a typed SDK is convenience, not a prerequisite.

## Planned install (once published)

```bash
npm install @clawie-dev/sdk
```

## Planned usage (sketch)

The SDK will mirror the [v1.0 REST surface](https://github.com/clawie-dev/docs/blob/main/reference/api.md):

```typescript
import { Clawie } from '@clawie-dev/sdk'

const c = new Clawie({ host: 'http://localhost:3333', token: process.env.CLAWIE_TOKEN })

// Create + execute a task (v1.0 surface)
const task = await c.tasks.create({
  intent: 'chat',
  payload: { prompt: 'Hello' },
})

// List pending approvals
const pending = await c.approvals.list({ status: 'pending' })

// Decide an approval (REST: POST /v1/tasks/:id/approval)
await c.approvals.decide(pending[0].taskId, { decision: 'approve' })

// Future (v1.x, post spec 016): high-level project orchestration on top
// of the task surface — c.projects.create({ brief, team, budget }) etc.
```

## Today, without the SDK

The v1.0 REST surface is intentionally small. `fetch` against the [five
documented endpoints](https://github.com/clawie-dev/docs/blob/main/reference/api.md)
is sufficient until the SDK ships:

```typescript
const res = await fetch('http://localhost:3333/v1/tasks', {
  method: 'POST',
  headers: { 'content-type': 'application/json' },
  body: JSON.stringify({ intent: 'echo', payload: 'world' }),
})
const task = await res.json()
```

Future sibling: `sdk-python`.

## License

MIT — see [LICENSE](LICENSE).
