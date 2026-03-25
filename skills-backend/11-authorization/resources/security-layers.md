# Security Layers Reference

## Authorization model

```
Incoming Request
│
├─ Layer 0: Authentication (Skill 10)
│   ├─ No valid credentials         → 401 Unauthorized
│   └─ Valid principal context      → continue
│
├─ Layer 1: Policy Check
│   ├─ Role / scope / policy fails  → 403 Forbidden
│   └─ Policy OK                    → continue
│
├─ Layer 2: Resource Existence (in service)
│   ├─ Resource not found           → 404 Not Found
│   └─ Resource exists              → continue
│
└─ Layer 3: Ownership Validation (in service)
    ├─ Principal has allowed override → execute operation
    ├─ Principal satisfies the resource access rule (owner, tenant member, collaborator, policy result) → execute operation
    └─ Rule not satisfied             → 403 Forbidden
```

---

## Test case matrix

| Principal | Action | Layer fails | Result |
|-----------|--------|:-----------:|:------:|
| Not authenticated | Any protected operation | Layer 0 | 401 |
| Authenticated, missing permission | Restricted endpoint | Layer 1 | 403 |
| Policy OK, resource does not exist | Edit any resource | Layer 2 | 404 |
| Policy OK, resource belongs to another principal | Edit another principal's resource | Layer 3 | 403 |
| Policy OK, owns the resource | Edit own resource | — | 2xx |
| Authenticated with explicit override | Edit protected resource | — | 2xx |

---

## Common mistakes

| Mistake | Consequence | Fix |
|---------|-------------|-----|
| Check ownership before existence | Returns 403 on non-existent resources, leaking data | Always 404 first, then 403 |
| Ownership logic in controller | Cannot be reused or tested in isolation | Move to service |
| Hardcoded role strings everywhere | Breaking changes when permissions evolve | Use constants, enums, scopes, or policy helpers |
| Mixed policy and ownership logic in one giant guard | Hard to reason about failures | Keep policy checks and ownership checks composable |
