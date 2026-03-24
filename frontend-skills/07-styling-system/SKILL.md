---
name: 07-styling-system
description: "Defines a scalable styling system with tokens, responsive layout primitives, theme persistence, and adaptable stack choices."
risk: low
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Styling becomes expensive when colors, spacing, responsive rules, and component variants are duplicated everywhere. This skill creates a stable token layer plus explicit stack and theme choices so the UI can grow without CSS collisions, visual drift, or framework lock-in.

**Descripcion (ES):**
El styling se vuelve costoso cuando colores, espaciados, reglas responsive y variantes de componentes se duplican por todas partes. Esta skill crea una capa estable de tokens mas decisiones explicitas de stack y tema para que la UI pueda crecer sin choques CSS, deriva visual ni dependencia excesiva de un framework.

Related resources:
- [styling-strategy.matrix.md](./resources/styling-strategy.matrix.md)

---

# 2. Skill Objective

**Objective (EN):**
Establish a styling architecture that is reusable, themeable, responsive, easy to maintain, and adaptable to the chosen styling stack.
- Use this skill when: Starting a frontend design system, cleaning a messy stylesheet layer, or adding theme and responsive rules that must survive project growth.
- Do not use this skill when: You only need a one-off page tweak inside an already consistent design system.

**Objetivo (ES):**
Establecer una arquitectura de estilos reutilizable, tematizable, responsive, facil de mantener y adaptable al stack de estilos elegido.
- Use esta skill cuando: Inicies un design system frontend, limpies una capa CSS caotica o agregues reglas de tema y responsive que deban sobrevivir al crecimiento del proyecto.
- No use esta skill cuando: Solo necesites un ajuste puntual dentro de un sistema visual ya consistente.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Design Tokens`: Color roles, spacing, radius, typography, elevation, motion, and breakpoints.
2. `Styling Strategy`: Utility CSS, CSS Modules, scoped CSS, styled APIs, component-library theming, or framework-native styles.
3. `Theme Requirements`: Light/dark mode, brand themes, persisted user preference, or accessibility constraints.
4. `Layout Primitives`: Containers, stacks, grids, surface patterns, and responsive shell requirements.

**Entradas (ES):**
1. `Design Tokens`: Roles de color, spacing, radius, tipografia, elevacion, motion y breakpoints.
2. `Styling Strategy`: Utility CSS, CSS Modules, scoped CSS, styled APIs, theming de librerias de componentes o estilos nativos del framework.
3. `Theme Requirements`: Light/dark mode, temas de marca, persistencia de preferencia del usuario o restricciones de accesibilidad.
4. `Layout Primitives`: Containers, stacks, grids, patrones de superficie y requisitos responsive del shell.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. A root token layer (`:root`, theme config, design-tokens file, or equivalent).
2. A documented responsive and theme-switch strategy.
3. Scoped component or feature styles that avoid global leakage.
4. A stack choice that is explicit instead of accidental.

**Salidas (ES):**
1. Una capa raiz de tokens (`:root`, configuracion de tema, archivo de design tokens o equivalente).
2. Una estrategia documentada para responsive y cambio de tema.
3. Estilos de componente o feature con alcance local que eviten filtraciones globales.
4. Una decision explicita del stack de estilos en lugar de una mezcla accidental.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Choose the styling stack intentionally:** Decide whether the project is utility-first, scoped CSS, module-based, styled API, or component-library themed before mixing patterns.
2. **Define tokens first:** Centralize color roles, spacing, typography, radius, elevation, and breakpoints before styling individual screens.
3. **Separate global from local:** Keep reset, body defaults, tokens, and layout primitives global; keep feature and component rules local or namespaced.
4. **Design responsive primitives:** Reuse containers, spacing scales, grids, and breakpoint rules instead of inventing one-off page layouts.
5. **Design theme switching explicitly:** Use CSS variables, data attributes, or framework theme providers instead of duplicating color values.
6. **Persist theme choice deliberately:** If user preference should survive reloads, document where and how it is stored.
7. **Integrate libraries through tokens:** If the project uses Tailwind, Prime, DaisyUI, Material, or another component library, align it through shared tokens and theme rules.
8. **Audit accessibility:** Verify contrast, focus states, motion preferences, and semantic color roles when the theme system changes.
9. **Adapt the pattern, not the literal example:** Rename files, token groups, layout primitives, themes, and style boundaries to match the target project's framework, styling strategy, and design language.

**Instrucciones (ES):**
1. **Elige el stack de estilos con intencion:** Decide si el proyecto sera utility-first, scoped CSS, basado en modulos, styled API o theming de libreria antes de mezclar patrones.
2. **Define tokens primero:** Centraliza roles de color, spacing, tipografia, radius, elevacion y breakpoints antes de estilizar pantallas individuales.
3. **Separa global de local:** Deja reset, defaults del body, tokens y primitivas de layout como globales; deja reglas de feature y componente como locales o namespaced.
4. **Disena primitivas responsive:** Reutiliza containers, escalas de espaciado, grids y reglas de breakpoint en lugar de inventar layouts de pagina para cada caso.
5. **Disena el cambio de tema de forma explicita:** Usa variables CSS, `data-theme` o providers del framework en lugar de duplicar valores de color.
6. **Persiste el tema con intencion:** Si la preferencia del usuario debe sobrevivir recargas, documenta donde y como se guarda.
7. **Integra librerias mediante tokens:** Si el proyecto usa Tailwind, Prime, DaisyUI, Material u otra libreria, alineala mediante tokens compartidos y reglas de tema.
8. **Audita accesibilidad:** Verifica contraste, estados de foco, preferencias de movimiento y roles semanticos de color cuando cambie el sistema de tema.
9. **Adapta el patron, no el ejemplo literal:** Renombra archivos, grupos de tokens, primitivas de layout, temas y limites de estilos para ajustarlos al framework, la estrategia de estilos y el lenguaje visual del proyecto objetivo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @07-styling-system to organize the visual foundation of this {Framework} project.
1. Choose a styling strategy, define a shared token layer, and create reusable responsive layout primitives.
2. Keep global reset and theme rules separate from feature styles and document how theme persistence works.
```

**Prompt (ES):**
```text
Usa la skill @07-styling-system para organizar la base visual de este proyecto {Framework}.
1. Elige una estrategia de estilos, define una capa compartida de tokens y crea primitivas reutilizables de layout responsive.
2. Mantén separadas las reglas globales de reset o tema y los estilos de features, y documenta como persiste la preferencia de tema.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
├── styles/
│   ├── tokens.{css|ts}
│   ├── theme.{css|ts}
│   ├── layout-primitives.{css|ts}
│   └── reset.{css}
└── components/
    └── {ComponentName}/
        ├── {ComponentName}.{ext}
        └── {ComponentName}.styles.{ext}
```

## Adaptation Checklist / Lista de Adaptacion

**Checklist (EN):**
- [ ] The styling stack was chosen intentionally instead of mixed accidentally.
- [ ] Tokens are defined once and reused across the app.
- [ ] Responsive layout primitives are shared instead of duplicated per screen.
- [ ] Theme changes preserve contrast, focus visibility, and motion accessibility.
- [ ] Theme persistence rules are documented when user preference survives reloads.
- [ ] Names, files, token groups, layout primitives, themes, and style boundaries were adapted to the target project instead of copying the example structure literally.

**Checklist (ES):**
- [ ] El stack de estilos fue elegido con intencion en lugar de mezclarse por accidente.
- [ ] Los tokens se definen una sola vez y se reutilizan en toda la app.
- [ ] Las primitivas responsive de layout se comparten en lugar de duplicarse por pantalla.
- [ ] Los cambios de tema conservan contraste, visibilidad del foco y accesibilidad de movimiento.
- [ ] Las reglas de persistencia del tema estan documentadas cuando la preferencia del usuario sobrevive recargas.
- [ ] Los nombres, archivos, grupos de tokens, primitivas de layout, temas y limites de estilos se adaptaron al proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
