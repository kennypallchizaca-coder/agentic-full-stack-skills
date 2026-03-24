# Validation Engine Matrix

Use this matrix to choose a form approach without tying the architecture to one framework.

| Approach | Typical stacks | Strengths | Best fit |
|---------|----------------|-----------|----------|
| Reactive form engine | Angular, Vue ecosystems | Built-in field state, nested groups, validators | Complex enterprise forms and dynamic field trees |
| Controlled inputs + schema validation | React, Preact, Solid | Explicit state flow, flexible composition | Medium-complexity forms with custom UI control |
| Schema-first form library | React Hook Form, VeeValidate, FormKit, generic wrappers | Fast setup, reusable schemas, plugin ecosystems | Repeated CRUD and settings forms |
| Native form plus lightweight enhancement | Astro islands, server actions, simple frameworks | Minimal client state, progressive enhancement | Content-heavy apps and simple submission flows |

## Decision guide

- Need arrays, nested groups, and status tracking: prefer a reactive or schema-first engine.
- Need progressive enhancement with minimal client JavaScript: keep the native form and add targeted enhancement.
- Need reusable validation across many forms: centralize rules in schemas or shared validators.
