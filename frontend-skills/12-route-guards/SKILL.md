---
name: 12-route-guards
description: "Protects routes with auth, guest and permission guards that wait for session bootstrap before redirecting."
risk: high
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Route guards should enforce navigation rules without flicker, loops, or stale session assumptions. Guards intercept navigation attempts and decide whether to allow, deny, or redirect based on session state and route metadata. Multiple guard types serve distinct purposes: **auth guards** protect private routes, **guest guards** block authenticated users from login/register pages, **role guards** restrict privileged areas, and **deactivation guards** prevent leaving routes with unsaved changes. This skill makes guards depend on explicit session state and route metadata instead of fragile browser storage checks.

**Descripción (ES):**
Los route guards deben hacer cumplir reglas de navegación sin flicker, loops ni supuestos viejos sobre la sesión. Los guards interceptan intentos de navegación y deciden si permitir, denegar o redirigir según el estado de sesión y la metadata de la ruta. Múltiples tipos de guard sirven para propósitos distintos: **auth guards** protegen rutas privadas, **guest guards** bloquean el acceso de usuarios autenticados a login/register, **role guards** restringen áreas privilegiadas y **deactivation guards** previenen salir de rutas con cambios sin guardar. Esta skill hace que los guards dependan de estado explícito de sesión y metadata de rutas, no de checks frágiles de almacenamiento del navegador.

Related resources:
- [guards.template.md](./resources/guards.template.md)

---

# 2. Skill Objective

**Objective (EN):**
Implement auth and guest route protection that cooperates with session hydration and fits the project's routing model.
- Use this skill when: Protecting private pages, preventing logged-in users from visiting login routes, applying role-based route access, or warning about unsaved form data.
- Do not use this skill when: The app is fully public and has no session-dependent navigation.

**Objetivo (ES):**
Implementar protección de rutas auth y guest que coopere con la hidratación de sesión y encaje con el modelo de routing del proyecto.
- Úsese cuando: Se protejan páginas privadas, se impida que usuarios logueados visiten rutas de login, se aplique acceso por rol o se advierta sobre datos de formulario sin guardar.
- No se use cuando: La app sea completamente pública y no tenga navegación dependiente de sesión.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Session Store`: Source of truth for `unknown`, `authenticated`, `guest`, and optionally roles. Must expose a definitive state — not raw token reads from browser storage.
2. `Route Metadata`: `requiresAuth`, `requiresGuest`, role/scopes, fallback paths. Each route should declare its protection level explicitly.
3. `Redirect Policy`: Login path, home path, forbidden path, and return URL behavior. Guard must preserve the user's intended destination when redirecting to login.

**Entradas (ES):**
1. `Session Store`: Fuente de verdad para `unknown`, `authenticated`, `guest` y opcionalmente roles. Debe exponer un estado definitivo — no lecturas crudas de tokens desde el storage del navegador.
2. `Route Metadata`: `requiresAuth`, `requiresGuest`, roles/scopes y rutas fallback. Cada ruta debe declarar su nivel de protección de forma explícita.
3. `Redirect Policy`: Ruta de login, home, forbidden y comportamiento de return URL. El guard debe preservar el destino deseado del usuario al redirigir al login.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Reusable auth, guest, role, and optionally deactivation guards.
2. Route configuration that depends on session state instead of ad-hoc checks scattered in components.
3. Redirect behavior that preserves intended destination when appropriate.

**Salidas (ES):**
1. Guards reutilizables de auth, guest, rol y opcionalmente de desactivación.
2. Configuración de rutas que depende del estado de sesión y no de checks improvisados dispersos en componentes.
3. Redirecciones que preservan el destino deseado cuando corresponde.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Wait for session bootstrap:** Guards must distinguish "session still loading" from "guest" to avoid false redirects. Never redirect during the `unknown` state.
2. **Use the central auth store/service:** Never make direct browser-storage reads the primary truth source for route protection. The guard should query a shared service or store that manages session state.
3. **Implement distinct guard types:** Auth guards protect private routes, guest guards protect login/register routes, and role guards protect privileged areas. Keep each guard focused on one concern.
4. **Choose the right protection strategy:** Apply by-authentication (private vs public), by-role (USER vs ADMIN), or mixed (layered auth → role guards) depending on the application's needs. Simpler apps need only auth vs guest; complex apps benefit from hierarchical strategies.
5. **Centralize auth logic in guards, not in components:** Never duplicate `if (!isAuthenticated()) redirect('/login')` inside component lifecycle hooks. Guards handle this once; components focus on their responsibility.
6. **Preserve intent when useful:** Redirect unauthenticated users to login with a return URL or equivalent router state so they arrive at their intended page after login.
7. **Consider deactivation guards:** For routes with forms or unsaved state, implement guards that warn users before navigating away. This prevents accidental data loss.
8. **Keep guard logic deterministic:** Avoid side effects beyond navigation decisions and shared session resets.
9. **Adapt the pattern, not the literal example:** Rename files, guards, route metadata, and redirect rules to match the target project's router, auth flow, and business language.

**Instrucciones (ES):**
1. **Esperar el bootstrap de sesión:** Los guards deben distinguir entre "sesión aún cargando" y "guest" para evitar redirecciones falsas. Nunca redirigir durante el estado `unknown`.
2. **Usar el store o servicio central de auth:** Nunca conviertas lecturas directas del storage del navegador en la fuente principal de verdad para proteger rutas. El guard debe consultar un servicio o store compartido que gestione el estado de sesión.
3. **Implementar tipos de guard distintos:** Auth guards para rutas privadas, guest guards para login/register y role guards para áreas privilegiadas. Mantén cada guard enfocado en una sola responsabilidad.
4. **Elegir la estrategia de protección adecuada:** Aplica por autenticación (privada vs pública), por rol (USER vs ADMIN) o mixta (guards de auth → rol apilados) según las necesidades de la aplicación. Apps simples solo necesitan auth vs guest; apps complejas se benefician de estrategias jerárquicas.
5. **Centralizar lógica auth en guards, no en componentes:** Nunca dupliques `if (!isAuthenticated()) redirect('/login')` dentro de lifecycle hooks de componentes. Los guards manejan esto una vez; los componentes se enfocan en su responsabilidad.
6. **Preservar intención cuando sirva:** Redirige usuarios no autenticados al login con return URL o estado equivalente del router para que lleguen a su página deseada tras el login.
7. **Considerar guards de desactivación:** Para rutas con formularios o estado sin guardar, implementa guards que adviertan al usuario antes de navegar. Esto previene pérdida accidental de datos.
8. **Mantener lógica determinista:** Evita side effects más allá de decisiones de navegación y resets compartidos de sesión.
9. **Adapta el patrón, no el ejemplo literal:** Renombra archivos, guards, metadata de rutas y reglas de redirección para ajustarlos al router, el flujo de auth y el lenguaje de negocio del proyecto objetivo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @12-route-guards to protect navigation in this {Framework} app.
1. Build auth and guest guards that wait for session bootstrap before redirecting.
2. Use route metadata and the central auth store instead of direct browser storage checks.
3. Consider deactivation guards for pages with forms.
```

**Prompt (ES):**
```text
Usa la skill @12-route-guards para proteger la navegación en esta app {Framework}.
1. Construye auth y guest guards que esperen el bootstrap de sesión antes de redirigir.
2. Usa metadata de rutas y el store central de auth en lugar de checks directos de storage del navegador.
3. Considera guards de desactivación para páginas con formularios.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
├── app/
│   └── router/
│       ├── guards/
│       │   ├── require-auth.{ext}
│       │   ├── require-guest.{ext}
│       │   ├── require-role.{ext}
│       │   └── unsaved-changes.{ext}
│       └── routes.{ext}
└── features/
    └── auth/
        └── store/
            └── auth.store.{ext}
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Guards do not redirect until session bootstrap has completed.
- [ ] Route protection depends on shared session state, not direct token reads from browser storage.
- [ ] Auth redirects preserve the intended destination when appropriate.
- [ ] Auth logic is centralized in guards, not duplicated inside component lifecycle hooks.
- [ ] Routes with unsaved changes warn users before navigation when applicable.
- [ ] Names, files, guards, route metadata, and redirect rules were adapted to the target project instead of copying the example structure literally.

**Checklist (ES):**
- [ ] Los guards no redirigen hasta que el bootstrap de sesión termine.
- [ ] La protección de rutas depende del estado compartido de sesión, no de lecturas directas del storage del navegador.
- [ ] Las redirecciones auth preservan el destino deseado cuando aplica.
- [ ] La lógica auth está centralizada en guards, no duplicada dentro de lifecycle hooks de componentes.
- [ ] Las rutas con cambios sin guardar advierten al usuario antes de navegar cuando aplica.
- [ ] Los nombres, archivos, guards, metadata de rutas y reglas de redirección se adaptaron al proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
