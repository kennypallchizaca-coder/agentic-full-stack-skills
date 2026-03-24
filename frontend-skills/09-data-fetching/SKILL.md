---
name: 09-data-fetching
description: "Centralizes API communication with reusable clients, repositories, transport-aware tests, and safe authentication-aware error handling."
risk: high
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Calling APIs directly from components quickly creates duplication, hidden auth bugs, and inconsistent error handling. This skill defines a shared network layer with one client, typed repositories, predictable handling of credentials, retries, failures, and transport-level tests. In modern reactive frameworks, data fetching also benefits from resource-based patterns (such as `resource()` or `rxResource()`) that automatically manage loading states, request cancellation, and reactivity to parameter changes.

**Descripción (ES):**
Consumir APIs directamente desde componentes crea rapido duplicacion, bugs de auth ocultos y manejo inconsistente de errores. Esta skill define una capa de red compartida con un solo cliente, repositorios tipados, tratamiento predecible de credenciales, reintentos, fallos y pruebas de transporte. En frameworks reactivos modernos, el consumo de datos tambien se beneficia de patrones basados en recursos (como `resource()` o `rxResource()`) que gestionan automaticamente estados de carga, cancelacion de requests y reactividad a cambios de parametros.

---

# 2. Skill Objective

**Objective (EN):**
Create a maintainable and testable HTTP layer that components can consume without knowing transport details, adapting to the target API and auth stack.
- Use this skill when: The app talks to REST, GraphQL, or internal API endpoints and needs reusable request behavior.
- Do not use this skill when: A tiny proof of concept only makes one disposable request.
- Security preference: Prefer cookie-based sessions with `withCredentials` over reading tokens from `localStorage`.

**Objetivo (ES):**
Crear una capa HTTP mantenible y testeable que los componentes puedan consumir sin conocer detalles del transporte, adaptandola al stack de API y auth objetivo.
- Usese cuando: La app hable con endpoints REST, GraphQL o APIs internas y necesite comportamiento reutilizable de requests.
- No se use cuando: Un proof of concept minimo solo haga una request descartable.
- Preferencia de seguridad: Prioriza sesiones por cookie con `withCredentials` por encima de leer tokens desde `localStorage`.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Base API Config`: Base URL loaded from environment configuration (not hardcoded), timeout, credentials mode, default headers.
2. `Auth Strategy`: Secure cookies, memory token, or documented bearer-token fallback.
3. `Error Contract`: Shared response shape for 4xx and 5xx failures that all repositories use.
4. `Testing Surface`: Repository success/failure cases, interceptor behavior, cancellation rules, and retry expectations that should remain stable.

**Entradas (ES):**
1. `Base API Config`: URL base cargada desde configuracion de entorno (no hardcodeada), timeout, modo de credenciales y headers por defecto.
2. `Auth Strategy`: Cookies seguras, token en memoria o bearer fallback documentado.
3. `Error Contract`: Forma compartida de respuesta para fallos 4xx y 5xx que todos los repositorios usen.
4. `Testing Surface`: Casos de exito/fallo de repositorios, comportamiento de interceptores, reglas de cancelacion y expectativas de retry que deban permanecer estables.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. A centralized API client instance configured with environment-based URL, timeout, and credentials.
2. Feature repositories or services that map endpoints to typed methods with explicit response interfaces.
3. Global response handling for `401` (trigger auth reset), `403` (show permission denied), and server failures (display user-friendly feedback).
4. A minimal test matrix that protects repository contracts, interceptor behavior, and failure mapping.

**Salidas (ES):**
1. Una instancia centralizada del cliente API configurada con URL de entorno, timeout y credenciales.
2. Repositorios o servicios por feature que mapean endpoints a metodos tipados con interfaces de respuesta explicitas.
3. Manejo global de respuestas para `401` (disparar reset de auth), `403` (mostrar permiso denegado) y fallos del servidor (mostrar feedback amigable al usuario).
4. Una matriz minima de pruebas que proteja contratos de repositorio, comportamiento de interceptores y mapeo de fallos.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Load base URL from environment config:** Centralize the API URL in environment variables or configuration files. Never hardcode URLs in services or components.
2. **Create one client per backend context:** Centralize timeout, JSON defaults, and credential behavior in a single shared client instance.
3. **Attach auth the safe way:** Prefer `withCredentials` or framework-native cookie support. Only inject bearer headers manually when the backend contract truly requires it.
4. **Wrap endpoints in repositories/services:** Components should call `UsersRepository.list()` rather than constructing raw URLs. Define explicit response interfaces for all endpoint return types.
5. **Normalize failures:** Map backend error payloads to one predictable shape and route `401` handling through the shared auth reset flow.
6. **Cancel stale requests automatically:** Use patterns like `switchMap` or framework-native resource APIs to cancel in-flight requests when parameters change. This prevents stale data from overwriting current results during rapid pagination or filter changes.
7. **Implement retry for transient failures:** Apply retry logic (2-3 attempts) for network errors or 5xx responses, with fallback values to prevent the UI from breaking entirely.
8. **Protect the transport boundary with tests:** Cover repository success/failure cases, `401` reset behavior, query-param construction, retry logic, and cancellation-sensitive flows without requiring a full browser stack.
9. **Keep components transport-agnostic:** UI code should focus on loading, empty, success, and error states, not on HTTP plumbing. Prefer resource-based patterns (`resource()`, `rxResource()`, query libraries) that provide built-in `isLoading()`, `value()`, and `error()` states.
10. **Adapt the pattern, not the literal example:** Rename files, clients, repositories, and auth hooks to match the target project's framework, API contract, and business language.

**Instrucciones (ES):**
1. **Cargar la URL base desde configuracion de entorno:** Centraliza la URL de API en variables de entorno o archivos de configuracion. Nunca hardcodees URLs en servicios ni componentes.
2. **Crear un cliente por contexto backend:** Centraliza timeout, defaults JSON y comportamiento de credenciales en una sola instancia compartida del cliente.
3. **Adjuntar auth de forma segura:** Prefiere `withCredentials` o soporte nativo de cookies del framework. Solo inyecta bearer headers manualmente cuando el contrato backend realmente lo exija.
4. **Envolver endpoints en repositorios o servicios:** Los componentes deberian llamar `UsersRepository.list()` en lugar de construir URLs crudas. Define interfaces de respuesta explicitas para los tipos de retorno de cada endpoint.
5. **Normalizar fallos:** Mapea los payloads de error backend a una forma predecible y envia el manejo de `401` por el flujo compartido de reset de auth.
6. **Cancelar requests obsoletas automaticamente:** Usa patrones como `switchMap` o APIs de recursos nativas del framework para cancelar requests en vuelo cuando los parametros cambien. Esto evita que datos obsoletos sobreescriban resultados actuales durante paginacion o cambios de filtro rapidos.
7. **Implementar retry para fallos transitorios:** Aplica logica de reintento (2-3 intentos) para errores de red o respuestas 5xx, con valores de fallback para evitar que la UI se rompa completamente.
8. **Proteger la frontera de transporte con pruebas:** Cubre exito/fallo de repositorios, reset por `401`, construccion de query params, retry y flujos sensibles a cancelacion sin depender de un stack completo de navegador.
9. **Mantener componentes agnosticos al transporte:** La UI debe enfocarse en loading, empty, success y error, no en plumbing HTTP. Prefiere patrones basados en recursos (`resource()`, `rxResource()`, librerias de query) que provean estados integrados como `isLoading()`, `value()` y `error()`.
10. **Adapta el patron, no el ejemplo literal:** Renombra archivos, clientes, repositorios y hooks de auth para ajustarlos al framework, el contrato API y el lenguaje de negocio del proyecto objetivo.

For repository/interceptor test scenarios, see [http-testing.matrix.md](./resources/http-testing.matrix.md).

Para escenarios de prueba de repositorios/interceptores, revisa [http-testing.matrix.md](./resources/http-testing.matrix.md).

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @09-data-fetching to structure API access in this {Framework} app.
1. Create a shared API client with environment-based URL, timeout, credentials and normalized error handling.
2. Expose typed repositories per feature so components never build raw HTTP requests inline.
3. Use resource-based data loading with automatic cancellation for paginated or filtered views.
4. Leave repository and interceptor tests covering auth failures and query behavior.
```

**Prompt (ES):**
```text
Usa la skill @09-data-fetching para estructurar el acceso API en esta app {Framework}.
1. Crea un cliente API compartido con URL de entorno, timeout, credenciales y manejo normalizado de errores.
2. Expon repositorios tipados por feature para que los componentes nunca construyan requests HTTP inline.
3. Usa carga de datos basada en recursos con cancelacion automatica para vistas paginadas o filtradas.
4. Deja pruebas de repositorio e interceptor cubriendo fallos de auth y comportamiento de queries.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
├── environments/
│   ├── environment.ts
│   └── environment.prod.ts
├── shared/
│   └── api/
│       ├── api-client.{ext}
│       ├── api-errors.{ext}
│       └── auth-interceptor.{ext}
└── features/
    └── {FeatureName}/
        ├── models/
        │   └── {feature}.model.{ext}
        └── api/
            ├── {feature}.repository.{ext}
            └── {feature}.repository.spec.{ext}
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Components never embed raw API URLs or auth header logic.
- [ ] Base API URL is loaded from environment configuration, not hardcoded.
- [ ] `401` responses trigger the shared session reset path.
- [ ] Stale requests are cancelled when parameters change (pagination, filters).
- [ ] Response types use explicit interfaces, not `any`.
- [ ] Repository or interceptor tests protect query construction, auth failures, and retry/cancellation-sensitive behavior.
- [ ] Browser token storage is not the default auth transport recommendation.
- [ ] Names, files, clients, repositories, and auth hooks were adapted to the target project instead of copying the example structure literally.

**Checklist (ES):**
- [ ] Los componentes nunca embeben URLs API crudas ni logica de auth headers.
- [ ] La URL base de API se carga desde configuracion de entorno, no hardcodeada.
- [ ] Las respuestas `401` disparan el camino compartido de reset de sesion.
- [ ] Las requests obsoletas se cancelan cuando los parametros cambian (paginacion, filtros).
- [ ] Los tipos de respuesta usan interfaces explicitas, no `any`.
- [ ] Las pruebas de repositorio o interceptor protegen construccion de queries, fallos de auth y comportamiento sensible a retry/cancelacion.
- [ ] El almacenamiento de tokens en el navegador no es la recomendacion por defecto.
- [ ] Los nombres, archivos, clientes, repositorios y hooks de auth se adaptaron al proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
