# Module Structure Template

Use this template to scaffold a domain module that is easy to understand at a glance, regardless of whether the project uses `src/modules/`, `src/features/`, `app/domains/`, `internal/`, or another stack-specific source root.

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
{source-root}/{modules-root}/{domain}/
├── transport/
│   ├── {domain}.controller.{ext} or router.{ext}
│   └── dto/
│       ├── create-{domain}.dto.{ext}
│       ├── update-{domain}.dto.{ext}
│       └── {domain}-response.dto.{ext}
├── application/
│   ├── {domain}.service.{ext}
│   └── use-cases/
├── domain/
│   ├── models/
│   └── policies/
├── infrastructure/
│   ├── {domain}.repository.{ext}
│   └── {domain}.entity.{ext}
├── tests/
└── index.{ext} or {domain}.module.{ext}
```

## Minimal variant

If the project is still small, a flatter module is also valid:

```text
{source-root}/{modules-root}/{domain}/
├── dto/
├── {domain}.controller.{ext}
├── {domain}.service.{ext}
├── {domain}.repository.{ext}
├── {domain}.entity.{ext}
├── index.{ext} or {domain}.module.{ext}
└── tests/
```

## When the module grows

- Add local subfolders such as `use-cases/`, `mappers/`, or `tests/` inside the same domain module.
- Do not create global top-level folders like `src/controllers/` or `src/services/` for the whole app.
- Keep external imports pointed at the module public entrypoint, not at deep internal files.
- Choose the depth that fits the project; do not force enterprise layering into a small service that does not need it yet.

## Shared and core folders

```
{source-root}/
├── core/
│   ├── config/
│   │   ├── app.config.{ext}
│   │   └── persistence.config.{ext}
│   ├── auth/
│   ├── observability/
│   └── persistence/
└── shared/
    ├── contracts/
    ├── middleware/
    │   ├── auth.middleware.{ext}
    │   └── error.middleware.{ext}
    ├── utils/
    │   └── pagination.util.{ext}
    └── types/
```

## Module clarity checklist

- [ ] Can I understand the module without opening another feature folder?
- [ ] Does every file that belongs to one domain stay inside this module?
- [ ] Are config, auth, observability, and shared helpers outside the domain modules?
- [ ] Do other modules import only the public entrypoint?

## Naming checklist

- [ ] Folder name: `lowercase-kebab-case` (e.g., `work-orders`, `customer-accounts`)
- [ ] Class names: `PascalCase` with layer suffix (e.g., `WorkOrderController`, `WorkOrderService`)
- [ ] File names: `lowercase-kebab-case` with layer suffix (e.g., `work-order.controller.ts`)
- [ ] Table/collection names: `plural_snake_case` (e.g., `work_orders`)
