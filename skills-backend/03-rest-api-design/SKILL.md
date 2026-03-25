---
name: 03-rest-api-design
description: "Defines resource-oriented HTTP contracts with predictable routes, status codes, envelopes, versioning, and OpenAPI discipline."
risk: low
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
REST APIs stay maintainable when they are stateless, resource-oriented, and documented as an explicit contract. This skill standardizes route naming, HTTP verb semantics, idempotency, query parameter design, response envelopes, versioning, and OpenAPI quality so clients can integrate without guessing.

**Descripción (ES):**
Las APIs REST se mantienen sanas cuando son stateless, orientadas a recursos y documentadas como un contrato explícito. Esta skill estandariza nombres de rutas, semántica de verbos HTTP, idempotencia, diseño de query parameters, envelopes de respuesta, versionado y calidad de OpenAPI para que los clientes puedan integrarse sin adivinar.

Related resources:
- [api-contract.template.md](./resources/api-contract.template.md)
- [contract-test-checklist.md](./resources/contract-test-checklist.md)
- [http-status-reference.md](./resources/http-status-reference.md)
- [openapi-starter.template.md](./resources/openapi-starter.template.md)
- [openapi-quality-checklist.md](./resources/openapi-quality-checklist.md)
- [transport-decision-guide.md](./resources/transport-decision-guide.md)

---

# 2. Skill Objective

**Objective (EN):**
Design a stable HTTP contract for resource-style APIs that is easy to document, test, consume, and evolve without breaking clients.
- Use this skill when: Defining CRUD endpoints, nested resources, pagination/filtering, or public/internal REST contracts.
- Do not use this skill when: The use case is better modeled as GraphQL, RPC/command endpoints, or real-time push streams.

**Objetivo (ES):**
Diseñar un contrato HTTP estable para APIs orientadas a recursos, fácil de documentar, probar, consumir y evolucionar sin romper clientes.
- Úsese cuando: Definas endpoints CRUD, recursos anidados, paginación/filtrado o contratos REST públicos o internos.
- No se use cuando: El caso encaje mejor como GraphQL, endpoints RPC/comando o streams de tiempo real.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Resource Model`: Resource names, ownership rules, and collection vs item boundaries.
2. `Operations`: Read, create, replace, partial update, delete, search, and filter requirements.
3. `Contract Rules`: Auth requirements, response envelope, versioning expectations, and sensitive-field exclusions.

**Entradas (ES):**
1. `Resource Model`: Nombres de recursos, reglas de ownership y límites entre colección e item.
2. `Operations`: Necesidades de lectura, creación, reemplazo, actualización parcial, eliminación, búsqueda y filtrado.
3. `Contract Rules`: Requisitos de auth, envelope de respuesta, expectativas de versionado y exclusiones de campos sensibles.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Standardized collection and item routes such as `/{version-prefix}/{resources}` and `/{version-prefix}/{resources}/{id}`, or the equivalent convention used by the target platform.
2. Clear verb, status-code, and idempotency behavior for each operation.
3. Stable success/error envelopes with pagination metadata where needed.
4. An OpenAPI or equivalent machine-readable contract that matches implementation intent.

**Salidas (ES):**
1. Rutas estandarizadas de colección e item como `/{version-prefix}/{resources}` y `/{version-prefix}/{resources}/{id}`, o la convención equivalente usada por la plataforma objetivo.
2. Comportamiento claro de verbos, códigos HTTP e idempotencia por operación.
3. Envelopes estables de éxito/error con metadata de paginación cuando aplique.
4. Un contrato OpenAPI o equivalente legible por máquina que refleje la intención de implementación.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Model the API around resources:** Use plural nouns, separate collection routes from item routes, and avoid action verbs in the path.
2. **Keep the contract stateless:** Each request must carry the information needed to process it. Do not rely on hidden session state to understand a route.
3. **Map verbs to intent carefully:** `GET` reads, `POST` creates, `PUT` replaces, `PATCH` partially updates, and `DELETE` removes. Recheck retry behavior against idempotency before choosing the verb.
4. **Put filters in query parameters:** Keep pagination, sorting, searching, and filtering in query params instead of inventing custom action routes.
5. **Normalize response shapes:** Use a consistent success envelope (for example `data`, `meta`, `message`, `timestamp`, `path`) and a consistent error envelope (for example `status`, `error`, `message`, `details`, `timestamp`, `path`).
6. **Return correct status codes:** Use `200`, `201`, `204`, `400`, `401`, `403`, `404`, `409`, and `500/503` intentionally. Never return `200` with an error body.
7. **Version deliberately:** Choose a clear versioning strategy that matches the platform and client ecosystem. Path-based versioning such as `/api/v1/` is common, but header or media-type versioning can be equally valid.
8. **Protect contract boundaries:** Do not expose passwords, secret tokens, internal flags, or persistence-only fields in API responses.
9. **Document the API as code:** Maintain OpenAPI/Swagger examples, schemas, and security requirements alongside the implementation so docs do not drift.
10. **Check the transport boundary:** If the use case depends on arbitrary graph reads, command-style semantics, or server push, confirm REST is still the right fit before forcing it.
11. **Adapt the pattern, not the literal example:** Rename files, layers, contracts, and integrations to match the target project's architecture, framework conventions, and business language.

**Instrucciones (ES):**
1. **Modela la API alrededor de recursos:** Usa sustantivos en plural, separa rutas de colección y de item, y evita verbos de acción en el path.
2. **Mantén el contrato stateless:** Cada request debe traer la información necesaria para procesarse. No dependas de estado de sesión oculto para entender una ruta.
3. **Mapea verbos a la intención correcta:** `GET` lee, `POST` crea, `PUT` reemplaza, `PATCH` actualiza parcialmente y `DELETE` elimina. Revisa el comportamiento ante reintentos antes de elegir el verbo.
4. **Pon los filtros en query parameters:** Deja paginación, orden, búsqueda y filtrado en query params en lugar de inventar rutas de acción.
5. **Normaliza la forma de las respuestas:** Usa un envelope consistente de éxito (por ejemplo `data`, `meta`, `message`, `timestamp`, `path`) y un envelope consistente de error (por ejemplo `status`, `error`, `message`, `details`, `timestamp`, `path`).
6. **Retorna códigos correctos:** Usa `200`, `201`, `204`, `400`, `401`, `403`, `404`, `409` y `500/503` con intención. Nunca devuelvas `200` con un body de error.
7. **Versiona de forma deliberada:** Elige una estrategia de versionado clara que encaje con la plataforma y el ecosistema de clientes. El versionado en path como `/api/v1/` es común, pero header o media type también pueden ser válidos.
8. **Protege los límites del contrato:** No expongas passwords, tokens secretos, flags internos ni campos solo de persistencia dentro de las respuestas.
9. **Documenta la API como código:** Mantén ejemplos, schemas y requisitos de seguridad en OpenAPI/Swagger junto a la implementación para que la documentación no derive.
10. **Revisa el límite del transporte:** Si el caso depende de lecturas de grafo arbitrarias, semántica tipo comando o server push, confirma que REST sigue siendo la mejor opción antes de forzarlo.
11. **Adapta el patrón, no el ejemplo literal:** Renombra archivos, capas, contratos e integraciones para ajustarlos a la arquitectura, las convenciones del framework y el lenguaje de negocio del proyecto objetivo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @03-rest-api-design to define the HTTP contract for `{ResourceName}`.
1. Create collection and item endpoints with correct verbs, status codes, envelopes, and versioning.
2. Produce an OpenAPI-ready contract and call out if this use case should not be modeled as REST.
```

**Prompt (ES):**
```text
Usa la skill @03-rest-api-design para definir el contrato HTTP de `{ResourceName}`.
1. Crea endpoints de colección e item con verbos, códigos, envelopes y versionado correctos.
2. Produce un contrato listo para OpenAPI y señala si este caso no debería modelarse como REST.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
└── modules/
    └── {resource}/
        ├── dto/
        ├── contracts/
        │   ├── {resource}.contract.md
        │   └── openapi.{yaml|json}
        ├── transport/
        │   └── {resource}.controller.{ext}
        └── application/
            ├── {resource}.service.{ext}
            └── {resource}.contract-test.{ext}
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Endpoints use plural resource nouns consistently.
- [ ] Query parameters handle pagination, sorting, and filtering instead of custom action routes.
- [ ] Status codes and idempotency rules match the chosen HTTP verbs.
- [ ] Success and error responses follow a stable envelope shape.
- [ ] The contract is documented in OpenAPI/Swagger or an equivalent artifact.
- [ ] Sensitive data never leaves the API response contract.
- [ ] REST was chosen intentionally instead of forcing a poor fit over GraphQL, RPC, or streaming.
- [ ] Names, files, layers, and integrations were adapted to the target project's conventions instead of copying the example structure literally.

**Checklist (ES):**
- [ ] Los endpoints usan sustantivos de recurso en plural de forma consistente.
- [ ] Los query parameters manejan paginación, orden y filtros en lugar de rutas de acción.
- [ ] Los códigos de estado y reglas de idempotencia coinciden con los verbos HTTP elegidos.
- [ ] Las respuestas de éxito y error siguen una forma de envelope estable.
- [ ] El contrato está documentado en OpenAPI/Swagger o un artefacto equivalente.
- [ ] Los datos sensibles nunca salen en el contrato de respuesta.
- [ ] REST fue elegido de forma intencional y no forzada frente a GraphQL, RPC o streaming.
- [ ] Los nombres, archivos, capas e integraciones se adaptaron a las convenciones del proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
