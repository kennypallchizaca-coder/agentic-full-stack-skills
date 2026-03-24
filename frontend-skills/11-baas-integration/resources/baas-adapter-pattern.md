# BaaS Adapter Pattern

Use this pattern to keep provider-specific SDK code behind stable capability boundaries.

## Core idea

- One provider bootstrap file initializes the SDK.
- One adapter per capability hides provider syntax.
- Feature code talks to adapters or repositories, not to raw SDK calls.

## Capability map

| Capability | Typical providers | Adapter responsibility |
|-----------|-------------------|------------------------|
| Auth | Firebase Auth, Supabase Auth, Appwrite Auth | Expose session/user state and auth actions |
| Database | Firestore, Supabase DB, PocketBase collections | Query and write typed domain data |
| Storage | Firebase Storage, Supabase Storage, Appwrite Storage | Upload, read metadata, generate safe URLs |
| Realtime | Firestore snapshots, Supabase channels, PocketBase realtime | Subscribe and unsubscribe with clean lifecycle |
| Functions | Cloud Functions, Edge Functions, custom backend | Execute privileged operations outside the client |

## Portable rules

- The provider client is initialized once.
- Privileged actions stay behind rules or server-side functions.
- Session lifecycle belongs to the auth flow layer.
- Route protection belongs to the routing layer.
