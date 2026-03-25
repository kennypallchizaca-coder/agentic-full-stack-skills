---
name: 11-authorization
description: "Enforces authorization with guards, policy checks and ownership validation so authenticated users can only perform allowed actions."
risk: high
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Authentication answers who the user is; authorization answers what that user may do. Modern APIs protect endpoints at multiple levels: **public** (no auth), **authenticated** (valid token required), **policy-restricted** (role, scope, permission, or policy required), and **ownership-validated** (resource belongs to the caller or the project defines an explicit privileged override). The most common model is RBAC (Role-Based Access Control), where users are assigned roles and roles define permissions, but this skill also fits scopes and policy helpers. This skill applies authorization checks across controllers and services so protected actions stay locked to the right principals, with clear separation between `401`, `403`, and `404` responses.

**Descripción (ES):**
La autenticacion responde quien es el usuario; la autorizacion responde que puede hacer. Las APIs modernas protegen endpoints a multiples niveles: **publico** (sin auth), **autenticado** (token valido requerido), **restringido por politica** (rol, scope, permiso o politica requerida) y **validado por ownership** (el recurso pertenece al caller o el proyecto define un override privilegiado explicito). El modelo mas comun es RBAC (Control de Acceso Basado en Roles), donde los usuarios reciben roles y los roles definen permisos, pero esta skill tambien encaja con scopes y policy helpers. Esta skill aplica controles de autorizacion en controladores y servicios para que las acciones protegidas queden realmente bloqueadas al principal correcto, con separacion clara entre respuestas `401`, `403` y `404`.

---

# 2. Skill Objective

**Objective (EN):**
Implement authorization checks that clearly separate `401 Unauthorized` from `403 Forbidden`, apply the principle of minimal privilege, and fit the project's permission model.
- Use this skill when: Protecting restricted routes, scoped resources, or actions that require a specific permission set.
- Do not use this skill when: The endpoint is intentionally public and has no protected behavior.
- Key distinction: `401` means "I don't know who you are" (missing or invalid token); `403` means "I know who you are but you cannot do this" (insufficient permission or the resource rule is not satisfied).

**Objetivo (ES):**
Implementar controles de autorizacion que separen claramente `401 Unauthorized` de `403 Forbidden`, apliquen el principio de minimo privilegio y encajen con el modelo de permisos del proyecto.
- Usese cuando: Se protejan rutas restringidas, recursos acotados o acciones que requieran permisos especificos.
- No se use cuando: El endpoint sea intencionalmente público y no tenga comportamiento protegido.
- Distincion clave: `401` significa "no se quien eres" (token ausente o invalido); `403` significa "se quien eres pero no puedes hacer esto" (permiso insuficiente o la regla del recurso no se cumple).

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Principal Context`: Authenticated user ID, roles, scopes, or claims extracted from the validated token.
2. `Permission Model`: RBAC, ABAC, scopes, ownership rules, tenancy rules, or policy checks.
3. `Protected Actions`: Endpoints, service methods, or commands that require authorization, classified by protection level (public, authenticated, policy, ownership).

**Entradas (ES):**
1. `Principal Context`: ID del usuario autenticado, roles, scopes o claims extraídos del token validado.
2. `Permission Model`: RBAC, ABAC, scopes, reglas de ownership, reglas de tenancy o politicas.
3. `Protected Actions`: Endpoints, metodos de servicio o comandos que requieren autorizacion, clasificados por nivel de proteccion (publico, autenticado, por politica, por ownership).

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Guards, decorators, middleware, or policy helpers that centralize permission logic.
2. Service-level authorization checks for ownership-sensitive actions with project-defined privileged override when applicable.
3. Deterministic `401`, `403`, and `404` responses following the correct security order: authenticate → authorize by policy → verify existence → validate ownership.

**Salidas (ES):**
1. Guards, decoradores, middleware o helpers de políticas que centralicen lógica de permisos.
2. Checks de autorizacion a nivel servicio para acciones sensibles por ownership con override privilegiado definido por el proyecto cuando aplique.
3. Respuestas deterministas `401`, `403` y `404` respetando el orden correcto de seguridad: autenticar → autorizar por politica → verificar existencia → validar ownership.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Require authentication first:** Authorization should run only after identity has been resolved. The validation chain is: valid token or session → policy check → resource existence → ownership when relevant.
2. **Apply minimal privilege:** Assign principals only the permissions they need. Baseline roles or scopes should come from the project's permission model, and every privilege elevation must be explicit and auditable.
3. **Centralize permission checks:** Use guards, decorators, middleware, or policies instead of scattering ad-hoc checks through controllers. Authorization logic scoped to specific resources belongs in the service layer, not the controller.
4. **Check existence before ownership:** Load the resource first, return `404` if it does not exist, and only then evaluate ownership or an allowed privileged override. This prevents leaking information about which resources exist to unauthorized users.
5. **Add ownership validation in services:** When a rule depends on who owns a resource, verify it where the resource is loaded and business decisions occur. Pass the authenticated principal explicitly from the controller to the service as a parameter.
6. **Implement privileged or policy overrides explicitly:** If the project defines elevated roles, scopes, or policy exemptions, model them in a clear early-return branch instead of hardcoding special cases throughout the codebase.
7. **Return correct status codes:** `401` when there is no valid authenticated principal; `403` when the principal exists but lacks permission. Never expose ownership details in error messages.
8. **Log denials safely:** Record denied attempts with request ID, principal ID, action, and resource ID for audit value, without exposing sensitive policy details to clients.
9. **Adapt the pattern, not the literal example:** Rename files, layers, contracts, and integrations to match the target project's architecture, framework conventions, and business language.

**Instrucciones (ES):**
1. **Exigir autenticacion primero:** La autorizacion solo debe ejecutarse despues de resolver la identidad. La cadena de validacion es: token o sesion validos → check de politica → existencia del recurso → ownership cuando corresponda.
2. **Aplicar minimo privilegio:** Asigna a cada principal solo los permisos necesarios. Los roles o scopes base deben salir del modelo del proyecto y toda elevacion de privilegios debe ser explicita y auditable.
3. **Centralizar permisos:** Usa guards, decoradores, middleware o politicas en lugar de esparcir checks improvisados en controladores. La logica de autorizacion acotada a recursos especificos pertenece a la capa de servicio, no al controlador.
4. **Verificar existencia antes del ownership:** Carga primero el recurso, devuelve `404` si no existe y solo despues evalua ownership o un override privilegiado permitido. Esto evita filtrar informacion sobre que recursos existen a usuarios no autorizados.
5. **Agregar ownership en servicios:** Cuando la regla depende de quien es dueno del recurso, validalo donde se carga el recurso y ocurre la decision de negocio. Pasa el principal autenticado explicitamente del controlador al servicio como parametro.
6. **Implementar overrides privilegiados o de politica de forma explicita:** Si el proyecto define roles elevados, scopes especiales o exenciones de politica, modelalos en una rama clara y temprana en lugar de hardcodear casos especiales por todo el codigo.
7. **Devolver codigos correctos:** `401` cuando no existe principal autenticado valido; `403` cuando si existe pero no tiene permiso. Nunca expongas detalles de ownership en mensajes de error.
8. **Registrar denegaciones con seguridad:** Guarda intentos denegados con request ID, principal ID, accion e ID del recurso para valor de auditoria, sin exponer detalles sensibles de la politica al cliente.
9. **Adapta el patron, no el ejemplo literal:** Renombra archivos, capas, contratos e integraciones para ajustarlos a la arquitectura, las convenciones del framework y el lenguaje de negocio del proyecto objetivo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @11-authorization to protect `{FeatureName}` actions.
1. Add guard or policy checks for roles/scopes at the route boundary.
2. Validate ownership inside the service before updating or deleting protected resources, with project-defined privileged override if one exists.
```

**Prompt (ES):**
```text
Usa la skill @11-authorization para proteger las acciones de `{FeatureName}`.
1. Agrega checks de guard o políticas por roles/scopes en el borde de la ruta.
2. Valida ownership dentro del servicio antes de actualizar o eliminar recursos protegidos, con override privilegiado definido por el proyecto si existe.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
├── core/
│   └── auth/
│       ├── request-auth.{ext}
│       └── authorization-policy.{ext}
└── modules/
    └── {feature}/
        ├── {feature}.controller.{ext}
        └── application/
            ├── {feature}.service.{ext}
            └── {feature}.authorization.{ext}
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Unauthenticated requests fail with `401`, not `403`.
- [ ] Permission rules are centralized and reusable, not scattered across controllers.
- [ ] Ownership-sensitive actions are checked in the service layer, not only in the UI.
- [ ] Privileged roles, scopes, or policy overrides are explicit and safe when the project defines them.
- [ ] Missing resources return `404` before any ownership denial.
- [ ] Error messages never reveal who the actual owner of a resource is.
- [ ] Baseline permissions follow the project's least-privilege model and privilege escalation is auditable.
- [ ] Names, files, layers, and integrations were adapted to the target project's conventions instead of copying the example structure literally.

**Checklist (ES):**
- [ ] Las requests no autenticadas fallan con `401`, no con `403`.
- [ ] Las reglas de permisos están centralizadas y son reutilizables, no dispersas en controladores.
- [ ] Las acciones sensibles por ownership se validan en la capa de servicio, no solo en la UI.
- [ ] Los roles, scopes u overrides privilegiados son explicitos y seguros cuando el proyecto los define.
- [ ] Los recursos inexistentes devuelven `404` antes de cualquier denegación por ownership.
- [ ] Los mensajes de error nunca revelan quién es el dueño real de un recurso.
- [ ] Los permisos base siguen el modelo de minimo privilegio del proyecto y la escalada de privilegios es auditable.
- [ ] Los nombres, archivos, capas e integraciones se adaptaron a las convenciones del proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
