---
name: 11-authorization
description: "Enforces authorization with guards, role checks and ownership validation so authenticated users can only perform allowed actions."
risk: high
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Authentication answers who the user is; authorization answers what that user may do. Modern APIs protect endpoints at multiple levels: **public** (no auth), **authenticated** (valid token required), **role-restricted** (specific role like ADMIN), and **ownership-validated** (resource belongs to the caller or caller has privileged bypass). The most common model is RBAC (Role-Based Access Control), where users are assigned roles and roles define permissions. This skill applies role-based and ownership-based checks across controllers and services so protected actions stay locked to the right principals, with clear separation between `401`, `403`, and `404` responses.

**Descripción (ES):**
La autenticación responde quién es el usuario; la autorización responde qué puede hacer. Las APIs modernas protegen endpoints a múltiples niveles: **público** (sin auth), **autenticado** (token válido requerido), **restringido por rol** (rol específico como ADMIN) y **validado por ownership** (el recurso pertenece al caller o el caller tiene bypass privilegiado). El modelo más común es RBAC (Control de Acceso Basado en Roles), donde los usuarios reciben roles y los roles definen permisos. Esta skill aplica controles por rol y por ownership en controladores y servicios para que las acciones protegidas queden realmente bloqueadas al principal correcto, con separación clara entre respuestas `401`, `403` y `404`.

---

# 2. Skill Objective

**Objective (EN):**
Implement authorization checks that clearly separate `401 Unauthorized` from `403 Forbidden`, apply the principle of minimal privilege, and fit the project's permission model.
- Use this skill when: Protecting admin routes, scoped resources, or actions that require a specific permission set.
- Do not use this skill when: The endpoint is intentionally public and has no protected behavior.
- Key distinction: `401` means "I don't know who you are" (missing or invalid token); `403` means "I know who you are but you cannot do this" (insufficient role or not the owner).

**Objetivo (ES):**
Implementar controles de autorización que separen claramente `401 Unauthorized` de `403 Forbidden`, apliquen el principio de mínimo privilegio y encajen con el modelo de permisos del proyecto.
- Úsese cuando: Se protejan rutas admin, recursos acotados o acciones que requieran permisos específicos.
- No se use cuando: El endpoint sea intencionalmente público y no tenga comportamiento protegido.
- Distinción clave: `401` significa "no sé quién eres" (token ausente o inválido); `403` significa "sé quién eres pero no puedes hacer esto" (rol insuficiente o no eres el dueño).

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Principal Context`: Authenticated user ID, roles, scopes, or claims extracted from the validated token.
2. `Permission Model`: RBAC (most common — roles grant permissions), ABAC (attribute-based — context-dependent rules), ownership rules, or policy checks. RBAC is preferred for most web applications due to its simplicity and scalability.
3. `Protected Actions`: Endpoints, service methods, or commands that require authorization, classified by protection level (public, authenticated, role, ownership).

**Entradas (ES):**
1. `Principal Context`: ID del usuario autenticado, roles, scopes o claims extraídos del token validado.
2. `Permission Model`: RBAC (más común — roles otorgan permisos), ABAC (basado en atributos — reglas dependientes de contexto), reglas de ownership o políticas. RBAC es preferido para la mayoría de aplicaciones web por su simplicidad y escalabilidad.
3. `Protected Actions`: Endpoints, métodos de servicio o comandos que requieren autorización, clasificados por nivel de protección (público, autenticado, por rol, por ownership).

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Guards, decorators, middleware, or policy helpers that centralize permission logic.
2. Service-level authorization checks for ownership-sensitive actions with ADMIN bypass.
3. Deterministic `401`, `403`, and `404` responses following the correct security order: authenticate → authorize by role → verify existence → validate ownership.

**Salidas (ES):**
1. Guards, decoradores, middleware o helpers de políticas que centralicen lógica de permisos.
2. Checks de autorización a nivel servicio para acciones sensibles por ownership con bypass ADMIN.
3. Respuestas deterministas `401`, `403` y `404` respetando el orden correcto de seguridad: autenticar → autorizar por rol → verificar existencia → validar ownership.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Require authentication first:** Authorization should run only after identity has been resolved. The validation chain is: valid token → role check → resource existence → ownership.
2. **Apply minimal privilege:** Assign users the lowest permission level by default. New accounts receive `USER` role; promotion to `ADMIN` must be explicit and auditable.
3. **Centralize permission checks:** Use guards, decorators, or policies instead of scattering ad-hoc role checks through controllers. Authorization logic scoped to specific resources belongs in the service layer, not the controller.
4. **Check existence before ownership:** Load the resource first, return `404` if it does not exist, and only then evaluate ownership or privileged bypass. This prevents leaking information about which resources exist to unauthorized users.
5. **Add ownership validation in services:** When a rule depends on who owns a resource, verify it where the resource is loaded and business decisions occur. Pass the authenticated user explicitly from the controller to the service as a parameter.
6. **Implement privileged bypass explicitly:** Allow `ADMIN` or the equivalent privileged role to bypass ownership checks in a clear early-return branch. Check ADMIN first to avoid unnecessary ownership logic.
7. **Return correct status codes:** `401` when there is no valid authenticated principal; `403` when the principal exists but lacks permission. Never expose ownership details in error messages (e.g., do not reveal who the actual owner is).
8. **Log denials safely:** Record denied attempts with request ID, user ID, action, and resource ID for audit value, without exposing sensitive policy details to clients.
9. **Adapt the pattern, not the literal example:** Rename files, layers, contracts, and integrations to match the target project's architecture, framework conventions, and business language.

**Instrucciones (ES):**
1. **Exigir autenticación primero:** La autorización solo debe ejecutarse después de resolver la identidad. La cadena de validación es: token válido → check de rol → existencia del recurso → ownership.
2. **Aplicar mínimo privilegio:** Asigna a los usuarios el nivel de permiso más bajo por defecto. Cuentas nuevas reciben rol `USER`; la promoción a `ADMIN` debe ser explícita y auditable.
3. **Centralizar permisos:** Usa guards, decoradores o políticas en lugar de esparcir checks de rol improvisados en controladores. La lógica de autorización acotada a recursos específicos pertenece a la capa de servicio, no al controlador.
4. **Verificar existencia antes del ownership:** Carga primero el recurso, devuelve `404` si no existe y solo después evalúa ownership o bypass privilegiado. Esto evita filtrar información sobre qué recursos existen a usuarios no autorizados.
5. **Agregar ownership en servicios:** Cuando la regla depende de quién es dueño del recurso, valídalo donde se carga el recurso y ocurre la decisión de negocio. Pasa el usuario autenticado explícitamente del controlador al servicio como parámetro.
6. **Implementar bypass privilegiado de forma explícita:** Permite que `ADMIN` o el rol privilegiado equivalente salte la validación de ownership mediante una rama temprana y clara. Verifica ADMIN primero para evitar lógica de ownership innecesaria.
7. **Devolver códigos correctos:** `401` cuando no existe principal autenticado válido; `403` cuando sí existe pero no tiene permiso. Nunca expongas detalles de ownership en mensajes de error (ej: no reveles quién es el dueño real).
8. **Registrar denegaciones con seguridad:** Guarda intentos denegados con request ID, user ID, acción e ID del recurso para valor de auditoría, sin exponer detalles sensibles de la política al cliente.
9. **Adapta el patrón, no el ejemplo literal:** Renombra archivos, capas, contratos e integraciones para ajustarlos a la arquitectura, las convenciones del framework y el lenguaje de negocio del proyecto objetivo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @11-authorization to protect `{FeatureName}` actions.
1. Add guard or policy checks for roles/scopes at the route boundary.
2. Validate ownership inside the service before updating or deleting protected resources, with ADMIN bypass.
```

**Prompt (ES):**
```text
Usa la skill @11-authorization para proteger las acciones de `{FeatureName}`.
1. Agrega checks de guard o políticas por roles/scopes en el borde de la ruta.
2. Valida ownership dentro del servicio antes de actualizar o eliminar recursos protegidos, con bypass ADMIN.
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
- [ ] Privileged roles bypass ownership explicitly and safely, checked before ownership logic.
- [ ] Missing resources return `404` before any ownership denial.
- [ ] Error messages never reveal who the actual owner of a resource is.
- [ ] New users receive the lowest role by default; privilege escalation is auditable.
- [ ] Names, files, layers, and integrations were adapted to the target project's conventions instead of copying the example structure literally.

**Checklist (ES):**
- [ ] Las requests no autenticadas fallan con `401`, no con `403`.
- [ ] Las reglas de permisos están centralizadas y son reutilizables, no dispersas en controladores.
- [ ] Las acciones sensibles por ownership se validan en la capa de servicio, no solo en la UI.
- [ ] Los roles privilegiados hacen bypass del ownership de forma explícita y segura, verificados antes de la lógica de ownership.
- [ ] Los recursos inexistentes devuelven `404` antes de cualquier denegación por ownership.
- [ ] Los mensajes de error nunca revelan quién es el dueño real de un recurso.
- [ ] Los usuarios nuevos reciben el rol más bajo por defecto; la escalada de privilegios es auditable.
- [ ] Los nombres, archivos, capas e integraciones se adaptaron a las convenciones del proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
