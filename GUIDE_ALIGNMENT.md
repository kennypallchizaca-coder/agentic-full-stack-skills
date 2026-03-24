# Guide Alignment

This file documents how the skills in this repository trace back to the source material in:

- `icc-ppw-frameworks-backend-main`
- `icc-ppw-frameworks-web-main`

It exists for maintenance provenance and alignment, not as a source-text mirror.

## Rights and provenance note

- These notes exist for maintenance and publication review only.
- Publishing this repository assumes the maintainer either authored the referenced teaching material or has permission or a compatible license to publish rewritten derivative guidance based on it.
- Do not copy source text, screenshots, branding assets, student submissions, or other third-party material into this repository unless publication rights and attribution requirements are documented.
- Keep references generic and repository-relative; do not publish personal workstation metadata or private filesystem paths.

## Alignment approach

The source guide is strongly oriented toward Angular on the frontend and Spring-style patterns on the backend. The skills in this repository intentionally preserve the same architectural intent, sequencing, and quality constraints while rewriting the instructions in framework-agnostic terms so they can be applied across runtimes without copying framework-specific syntax as if it were universal.

The documentation hierarchy in this repository is intentional:

- `README.md` gives the high-level overview and scope.
- `frontend-skills/README.md` and `skills-backend/README.md` act as operational indexes for the skill sets.
- `GUIDE_ALIGNMENT.md` is the provenance, source-tracing, and scope-register document.

## Alignment status

- `Direct`: The skill maps closely to one main practice, concept document, or tightly bounded concept cluster.
- `Synthesized`: The skill was derived from multiple documents or from repeated patterns shown across the guide.

## Backend skills

| Skill | Source guide files | Status | Notes |
|---|---|---|---|
| `01-project-bootstrap` | `docs/01_conceptos_backend.md`, `docs/02_arquitectura_backend.md`, `docs/14_despliegue_produccion.md` | Synthesized | Covers backend bootstrap, env-driven startup, and a basic liveness contract while leaving readiness depth to deployment. |
| `02-modular-project-structure` | `docs/02_arquitectura_backend.md` | Direct | Focused on feature-based structure and layer separation. |
| `03-rest-api-design` | `docs/03_api_rest_conceptos.md` | Direct | Maps REST resources, statelessness, verbs, idempotency, status codes, response envelopes, versioning, and OpenAPI discipline. |
| `04-service-layer` | `docs/04_controladores_servicios.md` | Direct | Mirrors controller/service separation, dependency injection intent, and explicit test seams for reusable use cases. |
| `05-data-persistence` | `docs/05_repositorios_bd.md`, `docs/05_b_instalacion_postgres_docker.md` | Direct | Combines repositories, ORM and migration-oriented persistence setup. |
| `06-dto-and-validation` | `docs/06_modelos_dtos_validacion.md` | Direct | Tracks DTO boundaries and strict validation. |
| `07-error-handling` | `docs/07_control_errores.md` | Direct | Aligns centralized exceptions and consistent error responses. |
| `08-entity-relationships` | `docs/08_relacion_entidades.md` | Direct | Aligns entity relations, foreign keys and serialization care. |
| `09-advanced-querying` | `docs/09_relacion_requestparam.md`, `docs/10_paginacion.md` | Direct | Combines query params and pagination into one skill. |
| `10-jwt-authentication` | `docs/11_autenticacion_autorizacion.md` | Direct | Covers password hashing, JWT claims and token validation. |
| `11-authorization` | `docs/12_roles_autorizacion.md`, `docs/13_ownership_validacion.md` | Direct | Includes RBAC, ownership validation, privileged bypass and proper 401/403/404 order. |
| `12-production-deployment` | `docs/14_despliegue_produccion.md` | Direct | Covers production-vs-dev differences, runtime hardening, reverse-proxy concerns, health visibility, monitoring, CI/CD, and rollback guardrails. |

## Frontend skills

| Skill | Source guide files | Status | Notes |
|---|---|---|---|
| `01-project-setup` | `angular/01-instalacion_configuracio/01-instalacion_configuracio.md`, `astro/01-instalacion_configuracio-astro.md` | Direct | Covers setup, base config, env handling, quality gates, and frontend delivery baseline. |
| `02-component-architecture` | `angular/02-fundamentos/02-fundamentos.md`, `astro/02-fundamentos-astro.md` | Synthesized | The guide teaches component fundamentals; this skill generalizes them into component boundaries, composition rules, and an optional container/presentational split. |
| `03-routing-strategy` | `angular/03-Navegacion/03-Navegacion.md`, `astro/03-navegacion-astro.md`, `docs/renderizado.html` | Synthesized | Maps layouts, nested routes, lazy navigation, and render-strategy tradeoffs across CSR, SSR, SSG, ISR, and islands. |
| `04-form-orchestration` | `angular/04-Formularios/04-Formularios.md` | Direct | Tracks form handling and validation flow. |
| `05-ui-feedback-system` | `angular/05-UI-Heuristicas/05-UI-Heuristicas.md`, `angular/06-UI-Heuristicas-impl/06-UI-Heuristicas-impl.md`, `docs/05-heristicas.md` | Direct | Combines heuristic guidance with concrete UI feedback, accessibility, focus, and copy guardrails. |
| `06-authentication-flow` | `angular/11-firebase/11-firebase.md`, `angular/12-guards-seguridad-rutas/12-guards-seguridad-rutas.md` | Synthesized | The guide covers session-sensitive routing and provider auth; the full session lifecycle skill was derived from both. |
| `07-styling-system` | `angular/07-Estilos/07-Estilos.md`, `angular/08-Estilos-Tema-Componentes/08-Estilos-Tema-Componentes.md` | Direct | Covers tokens, themes and scoped styles. |
| `08-state-management` | `angular/09-Consumos_servicos/09-Consumos_servicos.md`, `docs/angular-obserbables-rx.md` | Synthesized | The guide emphasizes reactive state and resources; the store strategy skill consolidates those patterns. |
| `09-data-fetching` | `angular/09-Consumos_servicos/09-Consumos_servicos.md`, `docs/angular-obserbables-rx.md` | Direct | Covers shared API clients, services, Rx flows, error handling, and transport-aware test cases. |
| `10-advanced-navigation` | `angular/10-mejoras-vsuales/10-mejoras-vsuales.md` | Direct | Includes URL pagination, breadcrumbs, hero summaries and visual navigation helpers. |
| `11-baas-integration` | `angular/11-firebase/11-firebase.md` | Synthesized | The source is Firebase-specific; the skill generalizes it into provider-capability adapters so the same architecture can apply to similar BaaS platforms. |
| `12-route-guards` | `angular/12-guards-seguridad-rutas/12-guards-seguridad-rutas.md` | Direct | Covers auth guards, guest guards and guarded navigation behavior. |

## Review outcome

- The repository aligns with the strongest conceptual sections of the source guide while remaining portable across stacks.
- The major synthesized areas are documented explicitly instead of being presented as one-to-one source translations.
- Backend ownership validation is treated as part of authorization instead of being left implicit.
- Frontend routing, feedback, and delivery guidance now cover broader application concerns than the original course segmentation.

## Recent hardening pass

The latest optimization pass focused on the weak areas identified in the comparison review and reinforced both the skills and their support resources.

- Frontend `01-project-setup`: Added a delivery baseline for lint, typecheck, build, and publish readiness from the setup concepts.
- Frontend `02-component-architecture`: Expanded the skill from a narrow smart/dumb framing into broader component-boundary and composition guidance.
- Frontend `03-routing-strategy`: Added render-strategy guidance tied to CSR, SSR, SSG, ISR, and islands.
- Frontend `04-form-orchestration`: Added dynamic forms, async checks, nested groups, and reusable validation-engine guidance.
- Frontend `05-ui-feedback-system`: Added heuristic and accessibility guardrails for focus, keyboard support, and clearer feedback copy.
- Frontend `07-styling-system`: Added stack-neutral styling strategy choices, responsive rules, and theme-persistence considerations.
- Frontend `09-data-fetching`: Added transport-aware testing guidance for repositories, interceptors, and cancellation flows.
- Frontend `11-baas-integration`: Reframed Firebase-specific setup into provider-capability adapter guidance with clearer auth-boundary separation.
- Backend `01-project-bootstrap`: Clarified the boundary between basic liveness at bootstrap time and deeper readiness checks during deployment.
- Backend `03-rest-api-design`: Added response-envelope consistency, OpenAPI quality gates, and an explicit transport decision boundary for non-REST cases.
- Backend `04-service-layer`: Added stronger DI guidance, reusable use-case boundaries, and a concrete service-testing strategy.
- Backend `12-production-deployment`: Added observability, CI/CD release gates, smoke checks, rollback criteria, runtime-selection guidance, and process-supervision templates.

## Known intentional synthesis

- React and Vue concepts in the source material are thinner than the Angular material, so the frontend library necessarily synthesizes some cross-framework guidance instead of claiming one-to-one source coverage.
- Backend operational guidance is broader in the concepts repository than in some individual implementation modules, so the deployment skill summarizes the stable production practices rather than mirroring framework-specific commands.

## Known gaps and non-goals

- Testing guidance exists inside several resources, but testing is not yet a standalone frontend or backend skill family.
- Frontend deployment guidance currently lives inside `01-project-setup` resources rather than a dedicated delivery skill.
- Backend advanced transports such as GraphQL, gRPC, WebSockets, and SSE are documented as decision boundaries, not as full skill tracks.
- The backend library is intentionally strongest for REST-style service APIs; event-driven or distributed-platform patterns are outside the current primary scope.
