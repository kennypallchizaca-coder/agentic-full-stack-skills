---
name: 03-routing-strategy
description: "Defines a portable routing strategy with layouts, rendering-aware route boundaries, lazy loading, nested routes and predictable fallback handling."
risk: medium
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Routing is the structural backbone of a frontend application. This skill organizes route trees, layouts, dynamic segments, render-mode boundaries, lazy loading, and fallback screens so navigation remains scalable and understandable across frameworks.

**Descripción (ES):**
El routing es la columna estructural de una aplicación frontend. Esta skill organiza arboles de rutas, layouts, segmentos dinámicos, fronteras de renderizado, lazy loading y pantallas fallback para que la navegación escale y siga siendo entendible entre frameworks.

---

# 2. Skill Objective

**Objective (EN):**
Design a route system that separates public and private areas while keeping performance, rendering strategy, and maintainability under control across different router architectures.
- Use this skill when: The application has multiple pages, nested layouts, or route-level code splitting.
- Do not use this skill when: A small widget or modal has no standalone navigation model.

**Objetivo (ES):**
Disenar un sistema de rutas que separe areas publicas y privadas mientras mantiene rendimiento, estrategia de renderizado y mantenibilidad bajo control en distintas arquitecturas de router.
- Úsese cuando: La aplicación tenga multiples paginas, layouts anidados o code splitting por ruta.
- No se use cuando: Un widget pequeño o modal no tenga un modelo de navegación propio.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Router Mechanism`: Framework router, file-based router, or equivalent navigation layer.
2. `Route Tree`: Public pages, protected pages, dynamic detail routes, and error views.
3. `Layout Needs`: Shells such as app layout, auth layout, dashboard layout, or public layout.
4. `Rendering Strategy`: CSR, SSR, SSG, ISR, islands, or equivalent route/runtime behavior expected by the product.

**Entradas (ES):**
1. `Router Mechanism`: Router del framework, file-based router o capa equivalente de navegación.
2. `Route Tree`: Paginas publicas, protegidas, rutas dinámicas de detalle y vistas de error.
3. `Layout Needs`: Shells como app layout, auth layout, dashboard layout o public layout.
4. `Rendering Strategy`: CSR, SSR, SSG, ISR, islands o comportamiento equivalente de runtime/ruta esperado por el producto.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. A structured route definition with nested layouts.
2. Lazy-loaded pages or route modules where appropriate.
3. Deterministic fallback behavior for unknown paths.
4. A documented decision about how routing and rendering cooperate in the target stack.

**Salidas (ES):**
1. Una definicion de rutas estructurada con layouts anidados.
2. Paginas o módulos lazy-loaded cuando corresponda.
3. Comportamiento fallback determinista para rutas desconocidas.
4. Una decision documentada sobre como cooperan routing y renderizado en el stack objetivo.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Map the route tree first:** Identify public, protected, detail, and fallback routes before writing code.
2. **Choose the render model intentionally:** Decide whether each route or shell is client-rendered, server-rendered, static, or island-based before wiring navigation behavior.
3. **Group routes by layout:** Place routes under the shell that owns the shared navigation and page frame.
4. **Lazy-load route boundaries:** Split large pages or modules at route boundaries to reduce initial bundle cost.
5. **Support dynamic segments intentionally:** Keep route params explicit and aligned with feature needs.
6. **Match link behavior to the stack:** Use router primitives, file-based conventions, prefetch, or native links according to the framework's navigation and rendering model.
7. **Add a final fallback route:** Unknown paths should land on a consistent not-found view instead of a blank screen.
8. **Adapt the pattern, not the literal example:** Rename files, route groups, layouts, and conventions to match the target router, framework, and navigation model.

**Instrucciones (ES):**
1. **Mapear primero el arbol de rutas:** Identifica rutas publicas, protegidas, de detalle y fallback antes de escribir codigo.
2. **Elegir intenciónalmente el modelo de renderizado:** Decide si cada ruta o shell sera client-rendered, server-rendered, estatico o basado en islands antes de cablear la navegación.
3. **Agrupar rutas por layout:** Coloca cada ruta bajo el shell que posee la navegación compartida y el marco visual correspondiente.
4. **Aplicar lazy loading en límites de ruta:** Divide paginas o módulos grandes en fronteras de ruta para reducir el costo del bundle inicial.
5. **Soportar segmentos dinámicos con intención:** Manten los params explícitos y alineados con las necesidades del feature.
6. **Alinear el comportamiento de enlaces con el stack:** Usa primitivas del router, convenciones file-based, prefetch o links nativos segun el modelo de navegación y renderizado del framework.
7. **Agregar una ruta fallback final:** Las rutas desconocidas deben aterrizar en una vista consistente de no encontrado y no en una pantalla en blanco.
8. **Adapta el patrón, no el ejemplo literal:** Renombra archivos, grupos de rutas, layouts y convenciones para ajustarlos al router, framework y modelo de navegación del proyecto objetivo.

For render-mode tradeoffs and framework examples, see [rendering-strategy.matrix.md](./resources/rendering-strategy.matrix.md).

Para tradeoffs de renderizado y ejemplos por framework, revisa [rendering-strategy.matrix.md](./resources/rendering-strategy.matrix.md).

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @03-routing-strategy to organize navigation in this {Framework} app.
1. Separate public and private routes under their corresponding layouts.
2. Pick a routing and rendering model that fits the stack and the product.
3. Apply lazy loading and a final not-found route so navigation stays scalable and safe.
```

**Prompt (ES):**
```text
Usa la skill @03-routing-strategy para organizar la navegación de esta app {Framework}.
1. Separa las rutas publicas y privadas bajo sus layouts correspondientes.
2. Elige un modelo de routing y renderizado que encaje con el stack y el producto.
3. Aplica lazy loading y una ruta final de no encontrado para que la navegación sea escalable y segura.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
{source-root}/
├── {router-root}/
│   └── routes.{ext}
├── {layout-root}/
│   ├── public-layout.{ext}
│   └── protected-layout.{ext}
└── {feature-root}/
    └── {feature-name}/
        └── routes.{ext}
```

If the stack uses file-based routing, the same separation can live in folders instead of explicit `routes.{ext}` files.

Si el stack usa routing basado en archivos, la misma separación puede vivir en carpetas en lugar de archivos explícitos `routes.{ext}`.

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Public and protected areas are grouped under clear layouts.
- [ ] Routing decisions respect the stack's rendering model instead of assuming SPA-only behavior.
- [ ] Route-level lazy loading is used where it meaningfully reduces initial load cost.
- [ ] Unknown paths resolve to a predictable not-found experience.
- [ ] Names, files, route groups, layouts, and conventions were adapted to the target project instead of copying the example structure literally.

**Checklist (ES):**
- [ ] Las areas publicas y protegidas están agrupadas bajo layouts claros.
- [ ] Las decisiones de routing respetan el modelo de renderizado del stack y no asumen comportamiento SPA por defecto.
- [ ] El lazy loading por ruta se usa donde realmente reduce el costo de carga inicial.
- [ ] Las rutas desconocidas resuelven una experiencia consistente de no encontrado.
- [ ] Los nombres, archivos, grupos de rutas, layouts y convenciones se adaptaron al proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
