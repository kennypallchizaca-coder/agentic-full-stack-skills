---
name: 04-form-orchestration
description: "Structures controlled or reactive forms with reusable válidation, dynamic fields, async checks, and safe submission behavior."
risk: medium
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Forms are one of the main entry points for user data. This skill standardizes how to collect input, válidate it, show field-level feedback, support dynamic sections, and prevent duplicate or malformed submissions across frontend frameworks.

**Descripción (ES):**
Los formularios son una de las principales puertas de entrada de datos del usuario. Esta skill estándariza como recoger input, válidarlo, mostrar feedback por campo, soportar secciones dinámicas y prevenir envios duplicados o malformados entre frameworks frontend.

Related resources:
- [dynamic-form-patterns.md](./resources/dynamic-form-patterns.md)
- [validation-engine.matrix.md](./resources/validation-engine.matrix.md)

---

# 2. Skill Objective

**Objective (EN):**
Build reliable forms that keep válidation, dynamic field structure, submission state, and rendering in sync across the target framework and válidation approach.
- Use this skill when: Implementing login forms, CRUD forms, settings forms, nested repeatable sections, or any multi-field submit flow.
- Do not use this skill when: A simple one-field search input can stay as lightweight local state.

**Objetivo (ES):**
Construir formularios confiables que mantengan sincronizados válidación, estructura dinámica de campos, estado de envío y render dentro del framework y enfoque de válidación objetivo.
- Úsese cuando: Implementes formularios de login, CRUD, settings, secciones repetibles anidadas o cualquier flujo de envío con varios campos.
- No se use cuando: Un input simple de búsqueda pueda quedarse como estado local liviano.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Form Engine`: Native reactive bindings, controlled inputs, schema-first form library, or the project's chosen form abstraction.
2. `Validation Schema`: Native válidators, schema layer, async válidators, or an equivalent válidation contract supported by the stack.
3. `Submission Flow`: The API or action that receives the final payload, plus the expected backend error shape.

**Entradas (ES):**
1. `Form Engine`: Bindings reactivos nativos, inputs controlados, libreria schema-first o la abstraccion de formularios elegida por el proyecto.
2. `Validation Schema`: Validadores nativos, capa de esquemas, válidadores asíncronos o un contrato equivalente soportado por el stack.
3. `Submission Flow`: La API o accion que recibe el payload final, mas la forma esperada de los errores backend.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. A controlled or reactive form component with explicit initial state.
2. Validation logic separated from raw DOM access.
3. Predictable submit-lock behavior, field-level error rendering, and server-error mapping.
4. Dynamic field arrays or nested groups modeled without ad-hoc branching.

**Salidas (ES):**
1. Un componente de formulario controlado o reactivo con estado inicial explícito.
2. Logica de válidación separada del acceso crudo al DOM.
3. Comportamiento predecible de bloqueo durante submit, renderizado de errores por campo y mapeo de errores del servidor.
4. Arrays de campos o grupos anidados modelados sin ramas improvisadas.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Model the form schema first:** Define allowed fields, defaults, nested groups, repeatable sections, and válidation rules before wiring UI inputs.
2. **Bind inputs through the form engine:** Avoid reading values manually from the DOM when the framework offers reactive or controlled bindings.
3. **Track field and submit state:** Support concepts such as touched, dirty, invalid, pending, and submitting when the stack provides them.
4. **Support async and server-aware válidation:** Handle async uniqueness checks, delayed válidation, and backend error mapping without scattering those rules inside button handlers.
5. **Show válidation close to the field:** Keep input errors near their source and reserve global alerts for submit-level failures.
6. **Prevent duplicate submits:** Disable or guard the submit action while the request is in flight.
7. **Align with the backend válidation contract:** Frontend válidation rules should mirror DTO constraints the API expects so both layers stay consistent.
8. **Extract reusable helpers intentionally:** Field mappers, error adapters, or schema factories belong in shared helpers when multiple forms reuse the same rules.
9. **Adapt the pattern, not the literal example:** Rename files, layers, schemas, helpers, and field contracts to match the target project's framework, UX rules, and business language.

**Instrucciones (ES):**
1. **Modela primero el esquema del formulario:** Define campos permitidos, valores por defecto, grupos anidados, secciones repetibles y reglas de válidación antes de conectar la UI.
2. **Enlaza inputs mediante el form engine:** Evita leer valores manualmente del DOM cuando el framework ofrece bindings reactivos o controlados.
3. **Rastrea estado de campos y submit:** Soporta conceptos como touched, dirty, invalid, pending y submitting cuando el stack los ofrezca.
4. **Soporta válidación asíncrona y errores del servidor:** Maneja chequeos de unicidad, válidación diferida y mapeo de errores backend sin dispersar esas reglas dentro de handlers de botones.
5. **Muestra válidación cerca del campo:** Mantén los errores de input junto a su origen y deja las alertas globales para fallos de submit.
6. **Previene submits duplicados:** Deshabilita o protege la accion de envío mientras la request siga en curso.
7. **Alinea con el contrato de válidación del backend:** Las reglas del frontend deben reflejar las restricciones que la API espera para que ambas capas sigan consistentes.
8. **Extrae helpers reutilizables con intención:** Field mappers, adaptadores de error o fabricas de schema deben vivir en helpers compartidos cuando varios formularios reutilicen las mismas reglas.
9. **Adapta el patrón, no el ejemplo literal:** Renombra archivos, capas, esquemas, helpers y contratos de campos para ajustarlos al framework, las reglas UX y el lenguaje de negocio del proyecto objetivo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @04-form-orchestration to implement the `{UseCase}` form in this {Framework} app.
1. Define a válidation schema, dynamic field structure, and backend error mapping before wiring the UI.
2. Bind the form through the framework's form engine, support async válidation, and lock submission while the payload is being sent.
```

**Prompt (ES):**
```text
Usa la skill @04-form-orchestration para implementar el formulario `{UseCase}` en esta app {Framework}.
1. Define un esquema de válidación, una estructura dinámica de campos y el mapeo de errores backend antes de conectar la UI.
2. Enlaza el formulario mediante el motor del framework, soporta válidación asíncrona y bloquea el submit mientras se envia el payload.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
└── features/
    └── {FeatureName}/
        ├── components/
        │   └── {FeatureName}Form.{ext}
        ├── válidation/
        │   ├── {feature}.schema.{ext}
        │   └── {feature}.error-map.{ext}
        └── helpers/ or form/
            └── {feature}.form-utils.{ext}
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Form values are not read through ad-hoc DOM queries.
- [ ] Validation rules are centralized and reusable.
- [ ] Dynamic sections or repeatable groups have an explicit structure instead of manual branching.
- [ ] Async válidation and backend error mapping are handled consistently.
- [ ] The submit action is guarded against duplicate requests.
- [ ] Names, files, layers, schemas, helpers, and field contracts were adapted to the target project instead of copying the example structure literally.

**Checklist (ES):**
- [ ] Los valores del formulario no se leen mediante consultas DOM improvisadas.
- [ ] Las reglas de válidación están centralizadas y son reutilizables.
- [ ] Las secciones dinámicas o grupos repetibles tienen una estructura explícita en lugar de ramas manuales.
- [ ] La válidación asíncrona y el mapeo de errores backend se manejan de forma consistente.
- [ ] La accion de submit esta protegida contra requests duplicadas.
- [ ] Los nombres, archivos, capas, esquemas, helpers y contratos de campos se adaptaron al proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
