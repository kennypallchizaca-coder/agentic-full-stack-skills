---
name: 02-component-architecture
description: "Defines portable component primitives and separation boundaries so frontend features stay reusable across different component models."
risk: low
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Frontend code becomes hard to move across projects when every framework-specific convention is treated like a universal law. This skill defines portable component primitives first, then uses composition and optional container/presentational separation to keep rendering, interaction, and orchestration understandable across frameworks.

**Descripcion (ES):**
El codigo frontend se vuelve dificil de mover entre proyectos cuando cada convencion de framework se trata como si fuera una ley universal. Esta skill define primero primitivas portables de componentes y luego usa composicion y una separacion opcional entre orquestacion y presentacion para mantener claro el render, la interaccion y la logica del feature.

Related resources:
- [component-primitives.matrix.md](./resources/component-primitives.matrix.md)
- [smart-dumb-pattern.template.md](./resources/smart-dumb-pattern.template.md)

---

# 2. Skill Objective

**Objective (EN):**
Build feature UI around explicit component boundaries that can adapt to the target framework's component, page, layout, and reactivity model.
- Use this skill when: A feature mixes page orchestration, reusable UI fragments, route state, API calls, or non-trivial interactions.
- Do not use this skill when: A tiny visual element already has no meaningful state, composition, or orchestration concerns.

**Objetivo (ES):**
Construir UI de features alrededor de limites explicitos de componentes que puedan adaptarse al modelo de componentes, paginas, layouts y reactividad del framework objetivo.
- Use esta skill cuando: Un feature mezcle orquestacion de pagina, fragmentos UI reutilizables, estado de ruta, llamadas API o interacciones no triviales.
- No use esta skill cuando: Un elemento visual pequeno ya no tenga preocupaciones reales de estado, composicion u orquestacion.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Component Primitives`: Page, layout, feature view, reusable UI component, slot/children contract, or island boundary used by the chosen stack.
2. `State Sources`: Route params, local reactive state, repositories, global stores, or server-provided props.
3. `Interaction Contract`: Props, inputs, slots, emitted events, callbacks, or render functions required by the visual layer.

**Entradas (ES):**
1. `Component Primitives`: Pagina, layout, vista de feature, componente UI reutilizable, contrato de slot/children o limite de island usado por el stack elegido.
2. `State Sources`: Route params, estado reactivo local, repositorios, stores globales o props entregadas por el servidor.
3. `Interaction Contract`: Props, inputs, slots, eventos emitidos, callbacks o funciones de render requeridas por la capa visual.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Clear feature boundaries between pages/layouts, orchestration code, and reusable rendering units.
2. Explicit contracts for child composition and user interactions.
3. A component model that can be tested and moved without leaking hidden framework assumptions.

**Salidas (ES):**
1. Limites claros entre paginas/layouts, codigo de orquestacion y unidades reutilizables de render.
2. Contratos explicitos para composicion de hijos e interacciones del usuario.
3. Un modelo de componentes que pueda probarse y moverse sin filtrar supuestos ocultos del framework.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Model the primitives first:** Decide what counts as page, layout, feature shell, reusable component, and composition boundary in the chosen framework before splitting files mechanically.
2. **Keep orchestration near the feature entry point:** Route parsing, repository calls, and feature-level state should live close to the page, view, route module, or island entry.
3. **Keep rendering contracts explicit:** Pass data and interactions through props, inputs, slots, render props, or callbacks instead of depending on hidden shared state.
4. **Use container/presentational split when it helps:** Treat smart/dumb separation as an optional pattern for features with side effects, not as a mandatory rule for every component.
5. **Localize framework-specific reactivity:** Signals, hooks, refs, watchers, stores, or server props should stay close to the orchestration boundary instead of leaking through every UI leaf.
6. **Compose intentionally:** Use children, content projection, slots, or partials for reusable structure; do not duplicate layout shells just because frameworks name composition differently.
7. **Test by boundary:** Presentational units should render from mocks alone; orchestration units should own route state, repository calls, and derived behavior.
8. **Adapt the pattern, not the literal example:** Rename files, layers, contracts, and interactions to match the target project's framework, feature boundaries, and business language.

**Instrucciones (ES):**
1. **Modela primero las primitivas:** Decide que cuenta como pagina, layout, shell del feature, componente reutilizable y limite de composicion en el framework elegido antes de dividir archivos de forma mecanica.
2. **Mantén la orquestacion cerca de la entrada del feature:** El parseo de rutas, las llamadas a repositorios y el estado del feature deben vivir cerca de la pagina, vista, modulo de rutas o entrada de island.
3. **Mantén explicitos los contratos de render:** Pasa datos e interacciones mediante props, inputs, slots, render props o callbacks en lugar de depender de estado compartido oculto.
4. **Usa separacion contenedor/presentacion cuando ayude:** Trata smart/dumb como un patron opcional para features con efectos secundarios, no como una regla obligatoria para todo componente.
5. **Localiza la reactividad especifica del framework:** Signals, hooks, refs, watchers, stores o props del servidor deben quedarse cerca del borde de orquestacion y no filtrarse por cada hoja visual.
6. **Compone con intencion:** Usa children, content projection, slots o parciales para estructuras reutilizables; no dupliques shells solo porque cada framework nombra distinto la composicion.
7. **Prueba por limite:** Las unidades presentacionales deben renderizarse solo con mocks; las unidades de orquestacion deben ser dueñas del estado de ruta, llamadas a repositorios y comportamiento derivado.
8. **Adapta el patron, no el ejemplo literal:** Renombra archivos, capas, contratos e interacciones para ajustarlos al framework, los limites del feature y el lenguaje de negocio del proyecto objetivo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @02-component-architecture to structure `{FeatureName}` in this {Framework} project.
1. Define the page, layout, orchestration, and reusable UI boundaries for the feature.
2. Keep framework-specific state near the feature entry point and expose explicit contracts to child components.
3. Use a container/presentational split only where side effects and orchestration justify it.
```

**Prompt (ES):**
```text
Usa la skill @02-component-architecture para estructurar `{FeatureName}` en este proyecto {Framework}.
1. Define los limites de pagina, layout, orquestacion y UI reutilizable del feature.
2. Mantén el estado especifico del framework cerca de la entrada del feature y expone contratos explicitos a los componentes hijos.
3. Usa separacion contenedor/presentacion solo donde la orquestacion y los efectos secundarios realmente lo justifiquen.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
└── features/
    └── {FeatureName}/
        ├── pages/ or views/
        │   └── {FeatureName}Page.{ext}
        ├── layouts/ or shells/
        │   └── {FeatureName}Layout.{ext}
        ├── components/
        │   ├── {FeatureName}Panel.{ext}
        │   └── {FeatureName}Item.{ext}
        ├── composables/ or hooks/ or state/
        │   └── use-{feature}.{ext}
        └── api/ or services/
```

## Adaptation Checklist / Lista de Adaptacion

**Checklist (EN):**
- [ ] The project distinguishes page/layout orchestration from reusable UI rendering.
- [ ] Child composition uses explicit props, inputs, slots, callbacks, or equivalent contracts.
- [ ] Container/presentational split is used intentionally, not mechanically.
- [ ] Framework-specific reactivity stays close to the feature boundary instead of leaking through every UI leaf.
- [ ] Names, files, layers, contracts, and interactions were adapted to the target project instead of copying the example structure literally.

**Checklist (ES):**
- [ ] El proyecto distingue entre orquestacion de pagina/layout y render reutilizable de UI.
- [ ] La composicion de hijos usa props, inputs, slots, callbacks o contratos equivalentes de forma explicita.
- [ ] La separacion contenedor/presentacion se usa con intencion y no de forma mecanica.
- [ ] La reactividad especifica del framework se mantiene cerca del limite del feature en lugar de filtrarse por cada hoja visual.
- [ ] Los nombres, archivos, capas, contratos e interacciones se adaptaron al proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
