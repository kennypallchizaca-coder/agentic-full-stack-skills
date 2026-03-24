# Universal Full-Stack Skills
### 24 bilingual skills for portable frontend and backend work
**Reusable `SKILL.md` guides derived from the concepts repository and rewritten for cross-stack use**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Frontend Skills](https://img.shields.io/badge/Frontend-12_Skills-blue)]()
[![Backend Skills](https://img.shields.io/badge/Backend-12_Skills-green)]()
[![Bilingual](https://img.shields.io/badge/Bilingual-EN%20%7C%20ES-orange)]()

---

## About this repository

This repository is a skill library, not a runnable application. It contains 24 `SKILL.md` guides designed to help an AI assistant implement consistent frontend and backend architecture across different projects.

The content is grounded in the source concepts from the `CONCEPTOS-FRONTEND-BACKEND` material, then rewritten into framework-adaptable patterns so the guidance can travel across stacks without copying one framework's syntax as if it were universal.

What you will find here:
- 12 frontend skills in [frontend-skills/README.md](./frontend-skills/README.md)
- 12 backend skills in [skills-backend/README.md](./skills-backend/README.md)
- Source mapping and maintenance provenance in [GUIDE_ALIGNMENT.md](./GUIDE_ALIGNMENT.md)
- Publication guidance in [SECURITY.md](./SECURITY.md) and [LICENSE](./LICENSE)

What this repository does not claim:
- It is not a complete cookbook for every framework-specific API.
- It is not a full transport catalog for GraphQL, gRPC, WebSockets, or SSE.
- It does not yet treat testing as its own standalone skill track; testing guidance lives inside resources attached to core skills.

---

## Quick start

1. Copy the relevant folder into your AI workspace.
2. Point the agent to a specific skill:

> "Use the **@03-routing-strategy** skill from `frontend-skills/` to organize layouts and rendering choices."

> "Use the **@04-service-layer** skill from `skills-backend/` to move business rules out of controllers."

3. Run `npm run validate` before publishing changes to ensure the repository stays structurally consistent.

---

## Repository map

| Area | Path | Purpose |
|---|---|---|
| Frontend skills | [frontend-skills/README.md](./frontend-skills/README.md) | Portable client-side patterns for setup, routing, forms, auth, feedback, styling, and data flows |
| Backend skills | [skills-backend/README.md](./skills-backend/README.md) | Portable server-side patterns for REST APIs, services, persistence, security, and deployment |
| Alignment guide | [GUIDE_ALIGNMENT.md](./GUIDE_ALIGNMENT.md) | Documents how the skills map back to the source concepts and where synthesis was necessary |
| Validator | [`scripts/validate-skills.mjs`](./scripts/validate-skills.mjs) | Checks structure, links, and JSON resources before publication |

---

## Library shape

```text
.
├── frontend-skills/
│   ├── 01-project-setup/
│   ├── 02-component-architecture/
│   └── ... 10 more frontend skill folders
├── skills-backend/
│   ├── 01-project-bootstrap/
│   ├── 02-modular-project-structure/
│   └── ... 10 more backend skill folders
├── GUIDE_ALIGNMENT.md
├── README.md
└── scripts/
    └── validate-skills.mjs
```

---

## Design principles

- Preserve the architectural intent of the source concepts while removing unnecessary framework lock-in.
- Prefer reusable boundaries over copy-pasted file names or one-stack conventions.
- Keep frontend and backend concerns explicit, especially around auth, validation, contracts, and delivery.
- Document known synthesis and known gaps instead of pretending the source material covered everything equally.
