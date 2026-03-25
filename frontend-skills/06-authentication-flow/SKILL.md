---
name: 06-authentication-flow
description: "Orchestrates session lifecycle, hydration, logout, and 401 recovery while keeping provider setup and route protection in separate layers."
risk: high
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Authentication is more than a login form. The frontend must restore session state on boot, react to expired sessions, coordinate protected navigation, and avoid unsafe token storage patterns. This skill defines that session lifecycle end to end while keeping provider SDK wiring and route protection in their own layers.

**Descripción (ES):**
La autenticación es mucho mas que un formulario de login. El frontend debe restaurar la sesión al arrancar, reaccionar a sesiónes expiradas, coordinar navegación protegida y evitar patrónes inseguros de almacenamiento de tokens. Esta skill define ese ciclo de sesión de punta a punta manteniendo el wiring del provider y la protección de rutas en capas separadas.

Boundary note:
- Skill 06 owns session lifecycle and hydration.
- Skill 11 owns provider SDK or BaaS integration.
- Skill 12 owns route protection and navigation enforcement.

Nota de límites:
- La Skill 06 es duena del ciclo de sesión y la hidratación.
- La Skill 11 es duena del SDK del provider o la integración BaaS.
- La Skill 12 es duena de la protección de rutas y del enforcement de navegación.

---

# 2. Skill Objective

**Objective (EN):**
Implement a reliable session flow for SPA or hybrid frontend applications that fits the chosen auth architecture.
- Use this skill when: Building login/logout flows, protected dashboards, or startup hydration for authenticated apps.
- Do not use this skill when: Authentication is fully delegated to a BaaS SDK that already exposes reactive session state and no custom session lifecycle is needed.
- Security preference: Prefer `httpOnly`, `secure`, `sameSite` cookies. Use `localStorage` or `sessionStorage` only if the architecture explicitly requires it and the tradeoff is documented.

**Objetivo (ES):**
Implementar un flujo de sesión confiable para aplicaciónes frontend SPA o hibridas que encaje con la arquitectura de auth elegida.
- Úsese cuando: Construyas flujos de login/logout, dashboards protegidos o hidratación inicial de apps autenticadas.
- No se use cuando: La autenticación este delegada por completo a un SDK BaaS que ya expone estado reactivo de sesión y no se necesite un ciclo de sesión propio.
- Preferencia de seguridad: Prioriza cookies `httpOnly`, `secure`, `sameSite`. Usa `localStorage` o `sessionStorage` solo si la arquitectura lo exige de forma explícita y el riesgo queda documentado.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Auth Endpoints`: `login`, `logout`, `me`, and optionally `refresh`.
2. `Session Transport`: Secure cookies, in-memory token, or documented fallback storage.
3. `Global State`: Store/service that exposes session status to the app shell and guards.

**Entradas (ES):**
1. `Auth Endpoints`: `login`, `logout`, `me` y opcionalmente `refresh`.
2. `Session Transport`: Cookies seguras, token en memoria o almacenamiento alternativo documentado.
3. `Global State`: Store/servicio que expone el estado de sesión al shell de la app y a los guards.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. An auth repository/service that talks to the backend or to the provider adapter.
2. A global session store with explicit states such as `unknown`, `authenticated`, and `guest`.
3. A hydration routine and logout workflow reused by guards and HTTP error handling.

**Salidas (ES):**
1. Un repositorio o servicio de auth que hable con el backend o con el adaptador del provider.
2. Un store global de sesión con estados explícitos como `unknown`, `authenticated` y `guest`.
3. Una rutina de hidratación y un flujo de logout reutilizados por guards y manejo de errores HTTP.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Create the auth repository:** Isolate `login`, `logout`, `me`, and `refresh` calls outside UI components.
2. **Model explicit session states:** The app should distinguish between "still checking session" and "definitely logged out".
3. **Hydrate on startup:** On app boot, call `/me`, `refresh`, or the provider-backed session adapter before rendering protected routes.
4. **Centralize logout:** A single `logout()` action must clear session state, trigger backend or provider logout if needed, and redirect safely.
5. **Handle `401` once:** Route HTTP `401` responses through the same logout/session reset path to avoid duplicated logic and stale UI state.
6. **Keep boundaries clear:** Provider wiring stays in Skill 11 and route enforcement stays in Skill 12 so session lifecycle remains portable.
7. **Adapt the pattern, not the literal example:** Rename files, flows, auth states, and integration points to match the target project's framework, session model, and business language.

**Instrucciones (ES):**
1. **Crea el repositorio de auth:** Aisla las llamadas `login`, `logout`, `me` y `refresh` fuera de los componentes UI.
2. **Modela estados de sesión explícitos:** La app debe distinguir entre "aun verificando sesión" y "definitivamente deslogueado".
3. **Hidrata al arrancar:** Al iniciar la app, llama a `/me`, `refresh` o al adaptador de sesión del provider antes de renderizar rutas protegidas.
4. **Centraliza logout:** Una única accion `logout()` debe limpiar el estado de sesión, ejecutar logout backend o del provider si aplica y redirigir de forma segura.
5. **Maneja `401` una sola vez:** Enruta las respuestas HTTP `401` por el mismo camino de logout o reset de sesión para evitar lógica duplicada y UI obsoleta.
6. **Mantén claros los límites:** El wiring del provider queda en la Skill 11 y el enforcement de rutas queda en la Skill 12 para que el ciclo de sesión siga siendo portable.
7. **Adapta el patrón, no el ejemplo literal:** Renombra archivos, flujos, estados de auth y puntos de integración para ajustarlos al framework, el modelo de sesión y el lenguaje de negocio del proyecto objetivo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @06-authentication-flow to implement session management in this {Framework} app.
1. Build an auth repository plus a global session store with `unknown`, `authenticated`, and `guest` states.
2. Hydrate the session on app startup, route every `401` through the same reset flow, and keep provider wiring and route protection in their own layers.
```

**Prompt (ES):**
```text
Usa la skill @06-authentication-flow para implementar gestion de sesión en esta app {Framework}.
1. Construye un repositorio de auth y un store global con estados `unknown`, `authenticated` y `guest`.
2. Hidrata la sesión al arrancar la app, envia cada `401` por el mismo flujo de reset y mantén el provider y la protección de rutas en capas separadas.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
└── features/
    └── auth/
        ├── api/
        │   └── auth.repository.{ext}
        ├── store/
        │   └── auth.store.{ext}
        ├── hooks/ or composables/
        │   └── use-session-bootstrap.{ext}
        └── components/
            └── LoginForm.{ext}
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] A page refresh preserves the real session state after hydration.
- [ ] Protected routes wait for session bootstrap before redirecting.
- [ ] Token persistence is not stored in `localStorage` unless the project documents that exception and accepts the risk.
- [ ] Provider SDK setup and route protection are not mixed into the same layer as session lifecycle.
- [ ] Names, files, flows, auth states, and integration points were adapted to the target project instead of copying the example structure literally.

**Checklist (ES):**
- [ ] Un refresh de página preserva el estado real de la sesión después de la hidratación.
- [ ] Las rutas protegidas esperan el bootstrap de sesión antes de redirigir.
- [ ] La persistencia de tokens no se guarda en `localStorage` salvo que el proyecto documente esa excepcion y acepte el riesgo.
- [ ] El setup del SDK del provider y la protección de rutas no se mezclan con la misma capa del ciclo de sesión.
- [ ] Los nombres, archivos, flujos, estados de auth y puntos de integración se adaptaron al proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
