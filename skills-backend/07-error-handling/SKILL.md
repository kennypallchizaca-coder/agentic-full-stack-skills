---
name: 07-error-handling
description: "Centralizes backend error handling so failures are logged consistently and clients receive safe, predictable error responses."
risk: medium
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Scattered try/catch blocks create inconsistent APIs and hide operational problems. This skill establishes a global error strategy that separates business exceptions from unexpected failures and translates both into stable response contracts.

**Descripción (ES):**
Los `try/catch` dispersos crean APIs inconsistentes y esconden problemas operativos. Esta skill establece una estrategia global de errores que separa excepciones de negocio de fallos inesperados y traduce ambos a contratos de respuesta estables.

---

# 2. Skill Objective

**Objective (EN):**
Standardize how the backend throws, logs, and returns errors across the project's client-facing transport boundary, especially HTTP APIs.
- Use this skill when: The project exposes HTTP endpoints or another client-facing transport that needs a stable error contract.
- Do not use this skill when: You are only writing throwaway scripts with no client-facing contract.

**Objetivo (ES):**
Estandarizar como el backend lanza, registra y devuelve errores a traves de la frontera de transporte orientada a clientes, especialmente APIs HTTP.
- Usese cuando: El proyecto exponga endpoints HTTP u otro transporte orientado a clientes que necesite un contrato de error estable.
- No se use cuando: Solo se escriban scripts descartables sin contrato hacia clientes.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Error Types`: Validation, not found, conflict, unauthorized, forbidden, external dependency failures.
2. `Logging Strategy`: Console, structured logger, APM, or centralized observability.
3. `Response Schema`: Standard error body expected by API clients.

**Entradas (ES):**
1. `Error Types`: Validación, no encontrado, conflicto, no autorizado, prohibido y fallos de dependencias externas.
2. `Logging Strategy`: Consola, logger estructurado, APM u observabilidad centralizada.
3. `Response Schema`: Cuerpo estándar de error esperado por clientes.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Domain/application error classes or enums.
2. A global exception filter, middleware, or handler for the client-facing transport.
3. Safe client responses plus actionable logs for operators.

**Salidas (ES):**
1. Clases o enums de errores de dominio o aplicación.
2. Un filtro, middleware o handler global de excepciones.
3. Respuestas seguras para clientes y logs accionables para operadores.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Define known error categories:** Distinguish **validation errors** (DTO format, missing fields), **business errors** (not-found, conflict, auth, domain-rule violations), and **technical errors** (database failures, external dependencies, unexpected exceptions). Each category maps to specific transport-level outcomes.
2. **Translate errors centrally:** Use a single middleware/filter/handler to map exceptions to HTTP status codes or the equivalent client-facing transport contract.
3. **Log with context:** Include request ID or correlation ID, route or operation name, actor, and dependency details when available, but avoid leaking secrets or PII.
4. **Separate expected from unexpected:** Business errors should be cleanly exposed; unknown errors should return generic `500` responses or the transport-equivalent internal failure contract.
5. **Keep controllers/services focused:** Throw meaningful errors and let the global layer decide how to serialize them.
6. **Reuse categories outside HTTP without forcing the same schema:** Background jobs or integrations can share error taxonomy and logging rules even if they do not return the HTTP envelope shown in this skill.
7. **Adapt the pattern, not the literal example:** Rename files, layers, contracts, and integrations to match the target project's architecture, framework conventions, and business language.

**Instrucciones (ES):**
1. **Definir categorias conocidas:** Distingue **errores de validacion** (formato del DTO, campos faltantes), **errores de negocio** (no encontrado, conflicto, auth, violaciones de reglas del dominio) y **errores tecnicos** (fallos de base de datos, dependencias externas, excepciones inesperadas). Cada categoria mapea a resultados concretos del transporte.
2. **Traducir errores en un punto central:** Usa un middleware, filtro o handler unico para convertir excepciones en codigos HTTP o en el contrato equivalente del transporte orientado a clientes.
3. **Loggear con contexto:** Incluye request ID o correlation ID, ruta u operacion, actor y detalles de dependencias cuando existan, pero sin filtrar secretos ni PII.
4. **Separar lo esperado de lo inesperado:** Los errores de negocio pueden exponerse limpiamente; los desconocidos deben devolver `500` generico o el contrato equivalente de fallo interno.
5. **Mantener foco en controladores y servicios:** Lanza errores significativos y deja que la capa global decida como serializarlos.
6. **Reutilizar categorias fuera de HTTP sin forzar el mismo schema:** Los jobs o integraciones pueden compartir taxonomia y logging aunque no devuelvan el envelope HTTP mostrado en esta skill.
7. **Adapta el patron, no el ejemplo literal:** Renombra archivos, capas, contratos e integraciones para ajustarlos a la arquitectura, las convenciones del framework y el lenguaje de negocio del proyecto objetivo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @07-error-handling to standardize backend failures.
1. Create application error types for validation, not-found, conflict and auth cases.
2. Add a global handler that logs context and returns a safe shared error schema.
```

**Prompt (ES):**
```text
Usa la skill @07-error-handling para estandarizar los fallos del backend.
1. Crea tipos de error de aplicación para validación, no encontrado, conflicto y auth.
2. Agrega un handler global que registre contexto y devuelva un esquema de error seguro y compartido.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
├── core/
│   ├── exceptions/
│   │   ├── GlobalExceptionHandler.{ext}
│   │   └── AppError.{ext}
└── modules/
    └── {feature}/
        └── {feature}.service.{ext}
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Unknown failures return a safe `500` response without stack traces in production.
- [ ] Validation and domain errors map to deterministic status codes.
- [ ] Logs contain enough context to debug incidents without exposing secrets.
- [ ] Names, files, layers, and integrations were adapted to the target project's conventions instead of copying the example structure literally.

**Checklist (ES):**
- [ ] Los fallos desconocidos devuelven un `500` seguro sin stack traces en producción.
- [ ] Los errores de validación y dominio mapean a códigos deterministas.
- [ ] Los logs contienen contexto suficiente para depurar sin exponer secretos.
- [ ] Los nombres, archivos, capas e integraciones se adaptaron a las convenciones del proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
