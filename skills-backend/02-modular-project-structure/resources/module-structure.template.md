# Module Structure Template

Use this template to scaffold a domain module that is easy to understand at a glance.

## Design rule

When someone opens the module folder, they should understand:

- where requests enter
- where business rules live
- where data access happens
- which files belong only to this domain
- which file is the public entrypoint for the rest of the app

Start simple and keep the full request-to-persistence flow inside the same domain folder.

## Recommended folder structure (per domain)

```
src/modules/{domain}/
├── dto/
│   ├── create-{domain}.dto.{ext}      ← Input for POST
│   ├── update-{domain}.dto.{ext}      ← Input for PUT/PATCH
│   └── {domain}-response.dto.{ext}    ← Output shape (no internals)
├── entities/
│   └── {domain}.entity.{ext}          ← Persistence model / ORM mapping
├── {domain}.controller.{ext}          ← HTTP controller / router / handler
├── {domain}.service.{ext}             ← Business rules and orchestration
├── {domain}.repository.{ext}          ← Database access only
├── {domain}.module.{ext} or index.{ext} ← Public entrypoint used by the app root
└── {domain}.spec.{ext}                ← Module tests
```

## When the module grows

- Add local subfolders such as `use-cases/`, `mappers/`, or `tests/` inside the same domain module.
- Do not create global top-level folders like `src/controllers/` or `src/services/` for the whole app.
- Keep external imports pointed at the module public entrypoint, not at deep internal files.

## Shared and core folders

```
src/
├── core/
│   ├── config/
│   │   ├── database.config.{ext}       ← DB connection setup
│   │   ├── jwt.config.{ext}            ← JWT secret + expiration
│   │   └── app.config.{ext}            ← General app settings
│   ├── auth/
│   └── logging/
└── shared/
    ├── middleware/
    │   ├── auth.middleware.{ext}       ← JWT filter (skill 10)
    │   └── error.middleware.{ext}      ← Global error handler (skill 07)
    ├── utils/
    │   └── pagination.util.{ext}       ← Paginated response builder
    └── types/
```

## Module clarity checklist

- [ ] Can I understand the module without opening another feature folder?
- [ ] Does every file that belongs to one domain stay inside this module?
- [ ] Are config, auth, logging, and shared helpers outside the domain modules?
- [ ] Do other modules import only the public entrypoint?

## Naming checklist

- [ ] Folder name: `lowercase-kebab-case` (e.g., `work-orders`, `customer-accounts`)
- [ ] Class names: `PascalCase` with layer suffix (e.g., `WorkOrderController`, `WorkOrderService`)
- [ ] File names: `lowercase-kebab-case` with layer suffix (e.g., `work-order.controller.ts`)
- [ ] Table/collection names: `plural_snake_case` (e.g., `work_orders`)
