---
name: 08-state-management
description: "Defines focused global state patterns that keep UI state, session state and server state clearly separated."
risk: high
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Global state becomes dangerous when it turns into a dumping ground. This skill defines how to keep client state small, explicit, and framework-appropriate while separating server cache, UI state, and session state. Modern frameworks offer reactive primitives — such as signals, resources, and observable-based data loaders — that manage server data without polluting client stores. Use those for server cache instead of manually syncing API responses into global state.

**Descripción (ES):**
El estado global se vuelve peligroso cuando se convierte en un basurero. Esta skill define cómo mantener el state del cliente pequeño, explícito y apropiado para cada framework, separando caché del servidor, estado UI y estado de sesión. Los frameworks modernos ofrecen primitivas reactivas — como signals, resources y cargadores de datos basados en observables — que gestionan datos del servidor sin contaminar los stores del cliente. Úsalas para caché del servidor en vez de sincronizar manualmente respuestas de API en el estado global.

Related resources:
- [global-store.template.md](./resources/global-store.template.md)

---

# 2. Skill Objective

**Objective (EN):**
Build small, intentional stores instead of one oversized global state container, adapting the pattern to the chosen state mechanism.
- Use this skill when: Multiple pages share UI/session state, or local prop drilling is becoming noisy.
- Do not use this skill when: The data belongs to a single component subtree and can stay local.
- Security note: Do not persist sensitive tokens in browser storage by default. Keep session truth in secure cookies or controlled memory when possible.

**Objetivo (ES):**
Construir stores pequeños e intencionales en lugar de un contenedor global gigantesco, adaptando el patrón al mecanismo de estado elegido.
- Úsese cuando: Varias páginas compartan estado de UI o sesión, o el prop drilling local ya genere ruido.
- No se use cuando: Los datos pertenezcan a un solo subárbol de componentes y puedan seguir locales.
- Nota de seguridad: No persistas tokens sensibles en almacenamiento del navegador por defecto. Mantén la verdad de la sesión en cookies seguras o memoria controlada cuando sea posible.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Shared State Types`: Session state, theme, UI preferences, wizard state, or feature filters.
2. `Shared State Mechanism`: Store, signal, service, reducer, or another explicit shared-state abstraction.
3. `Server Cache Strategy`: Resource APIs (`resource()`, `rxResource()`), query libraries (TanStack Query, SWR), or repository-level cache. These manage remote data reactively — with built-in loading/error states and automatic cancellation — and should be preferred over storing API results in global state.

**Entradas (ES):**
1. `Shared State Types`: Sesión, tema, preferencias UI, wizard state o filtros de features.
2. `Shared State Mechanism`: Store, signal, servicio, reducer u otra abstracción explícita de estado compartido.
3. `Server Cache Strategy`: APIs de recursos (`resource()`, `rxResource()`), librerías de query (TanStack Query, SWR) o cache a nivel de repositorio. Estos gestionan datos remotos de forma reactiva — con estados de carga/error integrados y cancelación automática — y deben preferirse sobre almacenar resultados de API en el estado global.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. One or more small stores with typed state and intent-based actions.
2. Clear separation between global client state and server-fetched data managed by resource/query layers.
3. Predictable hydration or bootstrap logic for shared state.

**Salidas (ES):**
1. Uno o varios stores pequeños con estado tipado y acciones orientadas a intención.
2. Separación clara entre state global del cliente y datos obtenidos del servidor gestionados por capas de resource/query.
3. Lógica predecible de hidratación o bootstrap del estado compartido.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Split state by concern:** Keep auth, theme, and feature UI state in separate stores unless they genuinely belong together.
2. **Prefer actions over direct mutation:** Expose methods such as `setSession`, `setFilters`, or `resetDraft` instead of leaking raw write access everywhere.
3. **Keep server data out of the store:** Prefer resource/query libraries for remote cache and use stores exclusively for client-owned state. Resource-based patterns (`resource()`, `rxResource()`, query hooks) handle reactivity, cancellation of stale requests, and loading/error states automatically — advantages that are lost when API results are manually copied into stores.
4. **Hydrate intentionally:** Rebuild store state from safe sources such as secure cookies, a `/me` endpoint, URL params, or documented persisted preferences. Never reconstruct session state from raw `localStorage` tokens as the primary source.
5. **Document persistence rules:** Only persist what the app truly needs across reloads, and never persist secrets casually.
6. **Adapt the pattern, not the literal example:** Rename files, stores, actions, and persistence rules to match the target project's framework, state library, and business language.

**Instrucciones (ES):**
1. **Separar el estado por responsabilidad:** Mantén auth, tema y estado UI de features en stores distintos salvo que realmente pertenezcan juntos.
2. **Preferir acciones sobre mutación directa:** Expón métodos como `setSession`, `setFilters` o `resetDraft` en vez de filtrar escritura cruda a cualquier lado.
3. **Dejar los datos del servidor fuera del store:** Prefiere librerías de resource/query para caché remota y usa stores exclusivamente para estado propiedad del cliente. Los patrones de recursos (`resource()`, `rxResource()`, query hooks) manejan reactividad, cancelación de requests obsoletas y estados de carga/error automáticamente — ventajas que se pierden cuando los resultados de API se copian manualmente a stores.
4. **Hidratar con intención:** Reconstruye el state desde fuentes seguras como cookies seguras, un endpoint `/me`, URL params o preferencias persistidas documentadas. Nunca reconstruyas el estado de sesión desde tokens crudos en `localStorage` como fuente principal.
5. **Documentar reglas de persistencia:** Persiste solo lo que la app necesita entre recargas y nunca secretos de forma casual.
6. **Adapta el patrón, no el ejemplo literal:** Renombra archivos, stores, acciones y reglas de persistencia para ajustarlos al framework, la librería de estado y el lenguaje de negocio del proyecto objetivo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @08-state-management to structure shared state in this {Framework} app.
1. Split session, theme and feature UI state into focused stores with typed actions.
2. Keep remote API data in resource/query layers (resource(), rxResource(), TanStack Query) instead of global stores.
```

**Prompt (ES):**
```text
Usa la skill @08-state-management para estructurar el estado compartido de esta app {Framework}.
1. Separa sesión, tema y estado UI de features en stores enfocados con acciones tipadas.
2. Mantén los datos remotos en capas resource/query (resource(), rxResource(), TanStack Query) en vez de stores globales.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
├── shared/
│   └── stores/
│       ├── auth.store.{ext}
│       ├── ui.store.{ext}
│       └── preferences.store.{ext}
└── features/
    └── {FeatureName}/
        └── state/
            └── {feature}.filters.store.{ext}
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Each store has a narrow responsibility and explicit actions.
- [ ] Remote API cache is managed by resource/query layers, not mixed into client UI state.
- [ ] Sensitive session data is not persisted in browser storage by default.
- [ ] Session state is hydrated from safe sources (cookies, `/me` endpoint), not from raw `localStorage` reads.
- [ ] Names, files, stores, actions, and persistence rules were adapted to the target project instead of copying the example structure literally.

**Checklist (ES):**
- [ ] Cada store tiene una responsabilidad estrecha y acciones explícitas.
- [ ] La caché remota de API se gestiona en capas resource/query, no mezclada en el estado UI del cliente.
- [ ] Los datos sensibles de sesión no se persisten por defecto en almacenamiento del navegador.
- [ ] El estado de sesión se hidrata desde fuentes seguras (cookies, endpoint `/me`), no desde lecturas crudas de `localStorage`.
- [ ] Los nombres, archivos, stores, acciones y reglas de persistencia se adaptaron al proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
