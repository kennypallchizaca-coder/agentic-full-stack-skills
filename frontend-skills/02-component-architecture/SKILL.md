---
name: 02-component-architecture
description: "Implements the Smart vs. Presentational (Dumb) Components architectural pattern. Isolates the visual interface layer from the HTTP/State business logic to maximize reusability across any frontend framework."
risk: low
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Components that directly fetch HTTP data, orchestrate Global Store injections, AND manage complex HTML visualization natively become unmaintainable monolithic entities instantly. This skill establishes the Container/Presentational design pattern delegating intelligent business logic strictly outside visual rendering hierarchies making testing significantly simpler natively.

**Descripción (ES):**
Los componentes que obtienen datos HTTP directamente, orquestan inyecciones del Store Global Y gestionan visualizaciones HTML complejas nativamente se convierten instantáneamente en entidades monolíticas inmantenibles. Esta skill establece el patrón de diseño Contenedor/Presentacional delegando la lógica de negocio inteligente estrictamente fuera de las jerarquías de renderizado visual, haciendo que las pruebas sean significativamente más simples.

---

# 2. Skill Objective

**Objective (EN):**
Decouple Frontend components into logical functional categories: Smart (Container) and Dumb (Presentational) components.
- Use this skill when: Building views demanding complex Server fetch lifecycles alongside deeply nested Custom UI Elements mapping explicit data.
- Do not use this skill when: Constructing single-hierarchy generic Utility Layout wrappers lacking state execution completely.

**Objetivo (ES):**
Desacoplar componentes del Frontend en categorías funcionales lógicas: componentes Smart (Contenedores) y Dumb (Presentacionales).
- Úsese cuando: Se construyen vistas que exigen ciclos de vida de obtención de Servidor complejos junto con Elementos UI Personalizados profundamente anidados mapeando datos explícitos.
- No se use cuando: Se construyen envolturas Utility Layout genéricas de una sola jerarquía carentes completamente de ejecución de estado.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Feature Domain`: E.g., UserProfiles or InvoiceCheckout.
2. `Data Source`: Network Fetcher or Global State store mapping target variables natively.

**Entradas (ES):**
1. `Feature Domain`: Ej. UserProfiles o InvoiceCheckout.
2. `Data Source`: Fetcher de Red o Store de Estado Global mapeando nativamente variables objetivo.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Pure Dumb Components executing UI mapping entirely reliant on explicit `Props` or `@Input()` definitions natively.
2. A Parent Smart View rendering HTTP lifecycles passing parsed target properties downward into the explicit Dumb interfaces efficiently.

**Salidas (ES):**
1. Componentes Dumb puros ejecutando mapeo UI apoyados completamente en definiciones explícitas de `Props` o `@Input()` nativamente.
2. Una Vista Smart Padre renderizando ciclos de vida HTTP pasando propiedades objetivo parseadas hacia abajo a las interfaces Dumb de manera eficiente.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Extract Dumb Components:** Generate generic functional interface components mapping exclusively visual code representations directly. They MUST NOT import Http clients (`axios`) or Routers (`vue-router`). Identify all interactive dependencies extracting them upward via `@Output()` EventEmitters or standard callback prop mapping parameters (e.g. `onDelete={() => {}}`).
2. **Engineer the Smart Container:** Implement a Top-Level Route view resolving asynchronous business dependencies (`useEffect` or `ngOnInit` HTTP fetches, reading Redux/Zustand logic). 
3. **Assemble Interaction:** Render the mapped Dumb interfaces downward within the Smart layout wrapper injecting required variable instances cleanly mapping return events recursively correctly.

**Instrucciones (ES):**
1. **Extraer Componentes Dumb:** Genera componentes de interfaz funcional genérica mapeando exclusivamente representaciones de código visual directamente. NO DEBEN importar clientes Http (`axios`) o Routers (`vue-router`). Identifica todas las dependencias interactivas extrayéndolas hacia arriba a través de EventEmitters `@Output()` o parámetros de mapeo de props de callback estándar (ej. `onDelete={() => {}}`).
2. **Ingeniar el Contenedor Smart:** Implementa una vista Route de Nivel Superior resolviendo dependencias asíncronas de negocio (obtenciones HTTP de `useEffect` o `ngOnInit`, lectura de lógica Redux/Zustand).
3. **Ensamblar Interacción:** Renderiza hacia abajo las interfaces Dumb mapeadas dentro de la envoltura layout Smart inyectando instancias de variables requeridas mapeando limpiamente eventos de retorno de manera recursiva correctamente.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @02-component-architecture to rebuild the `{ComponentName}` module into a robust Container mapping pattern natively.
1. Extract the pure HTML logic into a generic Dumb Component expecting `{ExpectedProps}` propagating an `onAction` callback parameter exactly.
2. Connect the asynchronous Service logic internally generating the Smart Wrapper View feeding explicit reactive variables natively without mutating them downward.
```

**Prompt (ES):**
```text
Usa la skill @02-component-architecture para reconstruir el módulo `{ComponentName}` en un patrón robusto de Contenedor nativamente.
1. Extrae la lógica HTML pura a un Componente Dumb genérico que espere `{ExpectedProps}` propagando un parámetro callback `onAction` exactamente.
2. Conecta la lógica de Servicio asíncrona generando internamente la Vista Envoltura Smart alimentando variables reactivas explícitas nativamente sin mutarlas hacia abajo.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
└── features/
    └── {EntityName}/
        ├── views/
        │   └── {EntityName}List.view.{ext}     ← Smart Container (Reads API)
        └── components/
            └── {EntityName}Table.{ext}         ← Dumb Presentational (Accepts list as Props)
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Confirm no HTTP Client or Router dependency executes inside the `components/` generic folder boundary natively.
- [ ] Validate Data Object state mutation entirely originates explicitly inside the View component logic exclusively avoiding bidirectional prop loops.
- [ ] Prove the Dumb Component renders identically using raw Mock Array object properties ignoring server availability entirely.

**Checklist (ES):**
- [ ] Confirmar que no se ejecuta ninguna dependencia de Cliente HTTP o Router dentro del límite de la carpeta genérica `components/` de forma nativa.
- [ ] Validar que la mutación de estado del Objeto de Datos se origina enteramente y de manera explícita dentro de la lógica del componente Vista evitando exclusivamente bucles de props bidireccionales.
- [ ] Demostrar que el Componente Dumb renderiza de forma idéntica usando propiedades crudas de un objeto Mock Array ignorando completamente la disponibilidad del servidor.
