# Transport Decision Guide

Use this note when a feature request is starting to stretch REST beyond a healthy fit.

| Need | Best fit | Why |
|------|----------|-----|
| Standard resource CRUD | REST | Predictable routes, cacheability, broad tooling support |
| Client-defined nested reads | GraphQL | Lets clients shape graph responses without route explosion |
| Explicit commands or remote procedures | RPC / command endpoint | Better when the operation is an action, not a resource |
| Server push or real-time updates | WebSocket / SSE | REST request-response is not built for ongoing streams |

## Stay in REST when

- The domain can be described as collections and items.
- Caching, idempotency, and standard HTTP semantics help clients.
- Pagination, filtering, and versioning are still understandable.

## Pause before forcing REST when

- Route names start turning into verbs such as `/approveInvoice` or `/syncInventory`.
- Clients need dozens of over-specialized endpoints just to assemble one screen.
- The server needs to push state changes to clients in real time.
- The operation is workflow-heavy and behaves more like a command than a resource mutation.

## Practical rule

If the request is still "create/read/update/delete a resource with a stable contract," keep REST.
If the problem is "execute a command," "query a graph," or "stream events," evaluate a different transport deliberately.
