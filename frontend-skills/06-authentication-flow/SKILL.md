---
name: 06-authentication-flow
description: "Orchestrates the complete Authentication Lifecycle in the client environment. Securely stores JWT tokens, hydrates global state across page reloads, and enforces systematic session termination."
risk: high
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Authentication is a multi-layered process. Successfully executing `/api/login` is merely step one; the frontend must permanently remember the user identity upon hard refreshes (`F5`), distribute the active role to guards (Skill 12), and purge credentials cleanly upon logout or `401` intercepts. This skill maps the precise cyclic flow of Session Management.

**Descripción (ES):**
La autenticación es un proceso de múltiples capas. Ejecutar exitosamente `/api/login` es solo el primer paso; el frontend debe recordar permanentemente la identidad del usuario ante recargas forzadas (`F5`), distribuir el rol activo a los guards (Skill 12), y limpiar las credenciales limpiamente ante un cierre de sesión (logout) o intercepciones `401`. Esta skill mapea el flujo cíclico preciso de la Gestión de Sesiones.

---

# 2. Skill Objective

**Objective (EN):**
Implement an isolated workflow handling User Identity bridging API responses, Local Storage, and the Global Store natively.
- Provide a persistent secure repository (e.g., `localStorage`, `sessionStorage`, or secure `cookies`) exclusively for the JWT Token matrix.
- Establish an App-Initialization Hook (Hydration Process) to restore identity logic deeply before interactive route components successfully render.
- Use this skill when: Building User login sessions (Login view, Dashboard panels) managing precise Access mechanisms globally.
- Do not use this skill when: Explicitly migrating internal configurations towards proprietary Third-Party Backend-as-a-Service (BaaS) ecosystems (e.g. Firebase Auth natively resolves tracking autonomously, ref Skill 11).

**Objetivo (ES):**
Implementar un flujo de trabajo aislado manejando la Identidad de Usuario conectando respuestas API, Local Storage y el Store Global nativamente.
- Proveer un repositorio seguro persistente (ej., `localStorage`, `sessionStorage` o `cookies` seguras) exclusivamente para la matriz del Token JWT.
- Establecer un Hook de Inicialización de la App (Proceso de Hidratación / Hydration) para restaurar la lógica de identidad profundamente antes de que los componentes interactivos de las rutas se rendericen con éxito.
- Úsese cuando: Se construyan sesiones de inicio de usuario (Vistas de Login, paneles de Dashboard) gestionando mecanismos de acceso precisos a nivel global.
- No se use cuando: Se migren configuraciones internas explícitamente hacia ecosistemas propietarios Backend-as-a-Service (BaaS) de terceros (ej. Firebase Auth resuelve nativamente este rastreo de forma autónoma, ref. Skill 11).

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Global Store`: The State Manager allocating universal `user` targets (Skill 08).
2. `Storage Mechanism`: `localStorage` binding library parsing logic or `Cookie` parameter parsing.

**Entradas (ES):**
1. `Global Store`: El Gestor de Estado asignando el destino universal del `usuario` (Skill 08).
2. `Storage Mechanism`: Librería o lógica adherida a `localStorage` procesando almacenamiento o lectura nativa de `Cookies`.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. An `AuthService` isolating the POST `/login` execution.
2. An `AuthStore` mapping specific observable `isAuthenticated` flags dynamically tracking state alongside explicit objects natively.
3. Universal Hydration root mapping triggering asynchronous generic verification algorithms pulling targets seamlessly.

**Salidas (ES):**
1. Un `AuthService` aislando de facto la ejecución pura sobre un POST `/login`.
2. Un `AuthStore` mapeando marcadores u observables dinámicos `isAuthenticated` junto con rastreos explícitos integrales al State.
3. Un proceso universal y único global de 'Hydration' mapeado a nivel root activando validaciones lógicas conectando a memoria sin causar ruidos y arrastrando las lecturas requeridas imperativamente.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Service Abstraction:** Define an `AuthRepository` implementing the network requests executing raw `/login`. Resolve the exact response targeting generic `tokens` successfully passing instances directly avoiding any interface DOM binding.
2. **Store Hydration Mechanism:** Code a routine triggered exactly once natively at application boot (`App.tsx useEffect[]`, Angular `APP_INITIALIZER`). Probe the current execution parsing `localStorage.getItem('token')`. If detected successfully, validate constraints natively executing an implicit HTTP `/me` read parsing mapping the object target logic cleanly into your global store array directly (`isAuthenticated = true`).
3. **Login Integration Logic:** Connect the isolated pure Form execution logic pointing target values to root actions natively. Ensure explicitly writing mapping instances toward Storage layers synchronously prior executing generic router re-direction.
4. **Logout Protocol Mapping:** Assemble an explicit global `logout()` function forcing three exact actions: [1] Destruction mappings targeting storage keys natively (`localStorage.removeItem`). [2] Overriding Generic global States tracking references to null. [3] Applying router constraints forcibly expelling user visibility natively mapping `/api` limits generic view execution securely.

**Instrucciones (ES):**
1. **Abstracción del Servicio:** Definir el `AuthRepository` que implemente y dispare peticiones puras asíncronas de red a `/login`. Resolver exactitudes desde lo local buscando tokens y aislando todo sin pegarlo en variables del DOM interactivas para una recepción simple.
2. **Mecanismos de Hidratación Lógica:** Codificar y enlazar rutinas originadas obligatoriamente a inicio del script raíz único de base del software una vez (`App.tsx useEffect[]`, `APP_INITIALIZER`). Probar una lectura inmediata sondeando el archivo nativo crudo o `localStorage.getItem('token')`. Ante detecciones confirmadas o presencias fiables se ejecuta implícitamente un lector local como HTTP `/me` procesando el target puro metiéndolo en cascada veloz adentro del almacén general e indicando el ok puro (`isAuthenticated = true`).
3. **Integración con Login en Pantalla:** Conectar operaciones de vista interactuando directo contra valores raíz. Confirmar anotaciones sincronizadas puritamente apuntadas grabando en memoria local todo lo generado nativo previniendo y resolviendo envíos al enrutador (router) al saltar pantallas u otros.
4. **Mapeo Protocolo de Salidas:** Trazar puramente e invocar genérica una salida estándar o función genérica log-out disparando acciones de bloque a 3 flujos: [1] Demolición de almacenamientos rastreados de claves ("tokens") (`removeItem`). [2] Borrado de variables locales o anulamiento a null en todo espacio común general al modelo local interactivo de States compartidos. [3] Aplicación certera final y purísima forzando saltos por el Enrutador/Router para botar miradas o permanencias estáticas prohibidas redirigiendo instantáneamente a fuera del sitio interior asegurando el proceso íntegro.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @06-authentication-flow to orchestrate Session state within this {Framework} ecosystem natively.
1. Define the exact Global AuthStore exposing the `isAuthenticated` reactive state integrating internal exact mutator hooks directly.
2. Force `login()` bindings executing generic API targets capturing tokens effectively mapping Browser Storage immediately gracefully parsing.
3. Validate targeted `Session Hydration` initialization routines injecting stored variables triggering synchronous application behavior exclusively correctly.
4. Encapsulate logout procedures mapping explicit data removal triggers alongside targeted navigational routing safely universally.
```

**Prompt (ES):**
```text
Usa la skill @06-authentication-flow para orquestar los estados de Sesión dentro de un ecosistema reactivo {Framework} de manera nativa.
1. Define específicamente la base de Global AuthStore exportando nativamente sus características `isAuthenticated` reactivas conectando ganchos exactos y directos (mutadores).
2. Forza y anexa un `login()` ejecutando el objetivo crudo asíncrono vía API guardando los mismos token o datos puros extraídos al instante en todo Local Browser Storage local detectado explícitamente y al instante limpiamente.
3. Valida en sí o activa la ejecución y mapeo del `Session Hydration` (Inicialización base o Hidratación) incorporando su búsqueda inyectando el valor salvado puramente hacia un gatilleo correcto que resuelva asíncronamente rutinas en memoria exclusivas correctísimas.
4. Encapsula y protege sus cierres o logouts eliminando referencias residuales con la destrucción de valores expuestos ejecutando simultáneamente en forma garantizada los saltos direccionales paralelos universalmente al enrutador con entera fiabilidad y firmeza de estructura.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
└── features/
    └── auth/
        ├── api/
        │   └── auth.repository.{ext}  ← HTTP POST calls handling server auth
        ├── store/
        │   └── auth.store.{ts}        ← Global logic capturing Session token lifecycle
        └── components/
            └── LoginForm.{ext}        ← Dumb UI triggering the Auth Store functions
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Ensure that forcing a literal Page Reload `F5` preserves specific Route Dashboard visibility correctly loading token variables exactly successfully universally natively securely.
- [ ] Determine that explicitly invoking internal generic target logout functions unmounts active protected view hierarchies immediately cleanly rendering guest configurations completely properly safely independently natively perfectly cleanly.
- [ ] Synchronize HTTP Network layer interceptor boundaries correctly bouncing tokens invoking common internal store `logout` variables explicitly avoiding redundant code loops efficiently natively locally.

**Checklist (ES):**
- [ ] Comprobar e impedir quiebres a visuales del Dashboard al recargar de lleno la pestaña entera literalmente vía la tecla del teclado `F5` asimilando o resolviendo internamente los parámetros token y datos en general pura fiablemente recargando correctamente su estancia en el localmente detectado scope interno exacto generalizado y global del proyecto seguro con entera base de forma segura.
- [ ] Ratificar que ejecutar de imprevisto una llamada `logout()` remota a interno, local u origen apaga íntegra y destructivamente las vistas y ramas protegidas (como perfiles de acceso) obligándolas a retirarse por completo limpiando puros estados internos asumiendo de una la pantalla general ajena deslogueada (Guest Mode) absolutamente al cierre completo local sin duda independiente de forma inmaculada sin pausas ni intercesiones visuales dudosas remarcando el proceso correctamente o un cierre explícito en red nativa.
- [ ] Interceptar de parte a contra-parte (Skill 09: data fetching) las señales en crudo `401 HTTP` coordinando u operando limpios destierros invocando esta MISMA y única variable lógica global purificando un cierre y reseteo al código principal de log out previendo re-escrituras largas asilando en paralelos flujos eficientes globales puros y cerrados sin duplicar llamadas.
