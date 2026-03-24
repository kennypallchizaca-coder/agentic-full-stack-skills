# Rendering Strategy Matrix

Use this guide when routing decisions depend on how pages are rendered, not only on URL shape.

## Decision table

| Mode | Best for | Watch out for |
|---|---|---|
| CSR | Internal apps, dashboards, auth-heavy SPAs | Slower first paint, SEO costs, client-only assumptions |
| SSR | Dynamic public pages, SEO-sensitive screens | Caching strategy, server cost, hydration mismatches |
| SSG | Marketing pages, docs, stable catalogs | Rebuild cost when content changes frequently |
| ISR / revalidation | Mostly-static content with timed refresh | Cache invalidation and freshness guarantees |
| Islands / partial hydration | Content-heavy pages with small interactive zones | Boundary complexity between static and interactive pieces |

## Routing implications

### SPA routers

- Prefer route guards, nested layouts, and code splitting at route boundaries
- Query params often act as UI state for pagination and filters

### File-based routers

- Directory structure becomes part of the contract
- Layout and loading/error files should follow framework conventions, not SPA habits

### Static-first runtimes

- Avoid assuming navigation state survives only in memory
- URLs, search params, and prefetch behavior become more important than client store hacks

## Questions to answer before implementation

- Is this screen public, protected, or hybrid?
- Does SEO matter for this route?
- Can the page be static, or does it need per-request freshness?
- Will the route be navigated mostly through links, forms, or programmatic transitions?
- Does the framework support prefetch, view transitions, or route loaders natively?

## Quick anti-patterns

- Using SPA-only redirect logic in a file-based or static-first router
- Forcing SSR everywhere when only one detail page needs it
- Keeping pagination only in local state when the URL should be shareable
- Copying `routerLink`-style patterns into frameworks that want plain links or file conventions
