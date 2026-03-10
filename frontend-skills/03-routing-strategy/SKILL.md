---
name: 03-routing-strategy
description: "Establishes a robust Routing Strategy for Single Page Applications (SPA). Implements lazy loading for performance optimization, structural routing layouts, and fallback 404 handlers."
risk: medium
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
A modern frontend Application relies heavily upon Browser History manipulation creating the illusion of deep nesting natively without server reloads. This skill imposes a highly structured Routing strategy configuring logical module Layouts, mapping dynamic parameter URL structures, and executing `Lazy Loading` logic preventing colossal initial javascript payloads.

**Descripción (ES):**
Una Aplicación frontend moderna depende en gran medida de la manipulación del Historial del Navegador creando la ilusión de anidamiento profundo nativamente sin recargas de servidor. Esta skill impone una estrategia de Routing altamente estructurada configurando Layouts modulares lógicos, mapeando parámetros dinámicos de estructuras URL y ejecutando lógica de `Lazy Loading` para evitar cargas iniciales colosales de javascript.

---

# 2. Skill Objective

**Objective (EN):**
Engineer a declarative application architecture routing standard paths rendering parent Layout structures effectively.
- Use this skill when: Setting up multi-page ecosystems involving internal Authenticated Dashboards explicitly distinct from Public Landing Pages.
- Do not use this skill when: Developing micro-components directly, or manipulating logic entirely within fixed Modal pop-up ecosystems.

**Objetivo (ES):**
Ingeniar una arquitectura de aplicación declarativa enrutando rutas estándar y renderizando estructuras Layout padre efectivamente.
- Úsese cuando: Se configuren ecosistemas multi-página que involucren Dashboards Autenticados internos explícitamente distintos de Landing Pages Públicas.
- No se use cuando: Se desarrollen micro-componentes directamente, o se manipule lógica de forma enteramente aislada dentro de ecosistemas de pop-ups Modales.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Router Mechanism`: E.g., React Router, Vue Router, Angular Routing Module.
2. `Views List`: Targeted Smart Components resolving explicit URL addresses cleanly.

**Entradas (ES):**
1. `Router Mechanism`: Ej., React Router, Vue Router, Angular Routing Module.
2. `Views List`: Componentes Smart objetivos resolviendo direcciones URL explícitas de manera limpia.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Standardized `Router` definition block injecting Lazy Loading Promise variables cleanly.
2. Encapsulated `MainLayout` wrapping static UI dependencies natively (e.g. permanent Sidebars/Navbars).
3. Base 404 Route handling invalid manual navigational inputs catching arbitrary string definitions completely.

**Salidas (ES):**
1. Bloque de definición estándar `Router` inyectando limpiamente variables Promesa de Lazy Loading.
2. `MainLayout` encapsulado envolviendo dependencias UI estáticas nativamente (ej. Sidebars/Navbars permanentes).
3. Ruta Base 404 manejando ingresos manuales inválidos de navegación, capturando definiciones de string aleatorias al 100%.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Initialize Lazy Rendering Logic:** Implement exact import parameter boundaries capturing Views asynchronously (`React.lazy(() => import())` or Vue `defineAsyncComponent`) enforcing optimal bundle sizes ignoring initial load mapping dependencies.
2. **Draft the Base Layouts:** Design structural Shell components holding universal navigation metrics natively injecting isolated `<Outlet />`, `<router-view>` or `<router-outlet>` variables dynamically.
3. **Assemble the Route Array:** Declare precise Array objects mapping URL Paths cleanly coupling them logically toward imported nested Lazy references natively. Include dynamic parsing indicators strictly (e.g. `path: '/items/:id'`).
4. **Append the Fallback Node:** Insert a catch-all wildcard string designation exactly at the file array conclusion rendering standardized 404 View Error pages gracefully preventing catastrophic white-screen renderings natively.

**Instrucciones (ES):**
1. **Inicializar Lógica Lazy Rendering:** Implementar límites exactos de importación capturando Vistas asíncronamente (`React.lazy(() => import())` o Vue `defineAsyncComponent`) forzando tamaños óptimos del bundle ignorando dependencias durante la carga inicial.
2. **Dibujar los Base Layouts:** Diseñar componentes Shell estructurales conteniendo la navegación universal, inyectando nativamente de forma dinámica las aisadas etiquetas `<Outlet />`, `<router-view>` o `<router-outlet>`.
3. **Ensamblar el Arreglo de Rutas:** Declarar objetos Array precisos mapeando limplamente Rutas URL, acoplándolas lógicamente con las referencias Lazy importadas. Incluir indicadores estrictos de parámetros dinámicos (ej. `path: '/items/:id'`).
4. **Agregar el Nodo Fallback:** Insertar una denominación comodín tipo "atrapar-todo" ("catch-all") exactamente al final del Array renderizando páginas estandarizadas de Error 404 preveniendo caídas de pantalla en blanco catastróficas.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @03-routing-strategy to map the navigational application flow securely in this {Framework} environment.
1. Implement a nested `<AuthLayout>` design architecture mapping internal Views properly injecting the outlet natively.
2. Define the exact path routing arrays targeting `{ViewComponents}` deploying strict Async Lazy logic parameters efficiently.
3. Apply standard catch-all wildcard parameters resolving manual typographical errors gracefully redirecting towards a `{NotFoundView}` correctly.
```

**Prompt (ES):**
```text
Usa la skill @03-routing-strategy para mapear el flujo navegacional seguro en este entorno {Framework}.
1. Implementa una arquitectura en diseño anidado `<AuthLayout>` mapeando las Vistas internas inyectando correctamente el puerto (outlet) nativo.
2. Define los parámetros exactos de rutas (arrays) hacia los `{ViewComponents}` desplegando estrictos parámetros Lógicos de Async Lazy eficientemente.
3. Aplica los parámetros estándar comodín atrapa-todo (catch-all) resolviendo de manera elegante los fallos tipográficos manuales redireccionando exactamente hacia un `{NotFoundView}`.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
├── app.router.{ts}             ← Index mapping entire Application routes
├── shared/
│   └── layouts/
│       ├── MainLayout.{ext}    ← Shell wrapper possessing persistent Headers
│       └── AuthLayout.{ext}    ← Unauthenticated simple Wrapper container
└── features/
    └── {EntityName}/
        └── routes.{ts}         ← Sub-module explicit route definitions
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Confirm viewing generic `/non/existent/path` correctly renders the explicit 404 Not Found component seamlessly.
- [ ] Prove entering `/dashboard` legitimately preserves persistent Universal components (Sidebar/Navbar) correctly avoiding un-needed continuous DOM recalculations natively.
- [ ] Ensure specific Views execute internal HTTP network fetches resolving Chunk payloads correctly preventing massive Main File index sizes securely.

**Checklist (ES):**
- [ ] Confirmar que ingresar genéricamente a `/non/existent/path` renderiza correctamente y de manera limpia el componente 404 No Encontrado.
- [ ] Demostrar que entrar a `/dashboard` verdaderamente preserva los componentes Universales permanentes (Sidebar/Navbar) previniendo recalcualciones continuas innecesarias del DOM.
- [ ] Asegurar que Vistas específicas ejecuten fetches de red HTTP resolviendo cargas ("Chunks") asíncronas de manera adecuada, reduciendo de forma segura el tamaño de descarga inicial del Archivo Principal (Main File index).
