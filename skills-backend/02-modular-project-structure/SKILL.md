---
name: 02-modular-project-structure
description: "Organizes the backend into self-contained feature modules so each domain is easy to understand, extend and test without opening unrelated folders."
risk: low
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
A professional backend grows by business domains, not by technical dumping grounds. This skill defines a domain-first structure so a teammate can open `catalog/`, `billing/`, `identity/`, `notifications/`, or any other business area and quickly understand where requests enter, where business rules live, where data access happens, and where tests belong. A domain module should be understandable in isolation — opening its folder should reveal the request entry point, the business logic, the persistence layer, the data contracts, and the public file that other modules are allowed to import.

**Descripción (ES):**
Un backend profesional crece por dominios del negocio, no por carpetas técnicas sin contexto. Esta skill define una estructura orientada a dominios para que alguien pueda abrir `catalog/`, `billing/`, `identity/`, `notifications/` o cualquier otra área del negocio y entender rápido dónde entra la petición, dónde vive la lógica, dónde está la persistencia y dónde se prueban esos cambios. Un módulo de dominio debe poder entenderse de forma aislada — al abrir su carpeta debe verse claramente el punto de entrada de la petición, la lógica de negocio, la persistencia, los contratos de datos y el archivo público que otros módulos pueden importar.

---

# 2. Skill Objective

**Objective (EN):**
Create a modular backend layout that scales cleanly across frameworks and languages while remaining easy to understand and adapt to the target project.
- Use this skill when: Starting a new backend, reorganizing a monolith, or preparing the project for multiple domains.
- Do not use this skill when: You only need to add a single helper file inside an already established module.

**Objetivo (ES):**
Crear una estructura backend modular que escale de forma limpia entre frameworks y lenguajes y siga siendo fácil de entender y adaptar al proyecto objetivo.
- Úsese cuando: Se inicia un backend nuevo, se reorganiza un monolito o se prepara el proyecto para múltiples dominios.
- No se use cuando: Solo se necesita agregar un archivo auxiliar dentro de un módulo ya definido.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Domain List`: Business areas such as `identity`, `catalog`, `orders`, `payments`, `support`, `reporting`, or any other bounded context in the project.
2. `Framework Conventions`: The runtime's module, package, container, or dependency-boundary rules.
3. `Shared Concerns`: Logging, config, auth, database, and utilities.

**Entradas (ES):**
1. `Domain List`: Áreas del negocio como `identity`, `catalog`, `orders`, `payments`, `support`, `reporting` o cualquier otro contexto delimitado del proyecto.
2. `Framework Conventions`: Reglas de módulos o contenedores del framework usado.
3. `Shared Concerns`: Logging, configuración, autenticación, base de datos y utilidades.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. A feature-based folder tree under the project source root (`src/`, `app/`, `internal/`, or the stack equivalent).
2. Clear placement rules so single-domain files stay inside the module and cross-cutting code moves to `core/`, `shared/`, `common/`, or the project equivalent.
3. A predictable root composition layer for route/module registration plus a clear public boundary per module.

**Salidas (ES):**
1. Un árbol de carpetas orientado a features dentro de la raíz de código del proyecto (`src/`, `app/`, `internal/` o el equivalente del stack).
2. Reglas claras para que los archivos de un solo dominio vivan dentro del módulo y lo transversal vaya a `core/`, `shared/`, `common/` o el equivalente del proyecto.
3. Una capa raíz predecible para registrar rutas o módulos y un límite público claro por módulo.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Make the domain the first organizing rule:** Create one folder per business area under the source root using the naming style that fits the stack, for example `src/modules/`, `src/features/`, `app/domains/`, or `internal/`.
2. **Model bounded contexts, not demo domains:** Organize around the real business areas of the project such as `catalog`, `billing`, `identity`, `fulfillment`, `reporting`, or `integrations`, not around tutorial-only examples.
3. **Keep the request flow inside the module:** Place the controller or handler, service or use case, repository, DTOs, entities, and tests beside the same domain so the full story can be read in one place.
4. **Move only true cross-cutting code out:** Config, auth, logging, middleware, observability, shared utilities, and framework bootstrapping belong in `core/`, `shared/`, `common/`, or their equivalent.
5. **Expose a public boundary:** Import or register a feature through `index.{ext}`, `{domain}.module.{ext}`, package exports, or the framework equivalent instead of deep-importing internal files from another module.
6. **Allow module depth to scale:** A small project can keep `controller`, `service`, and `repository` files directly inside the domain folder. A larger project can split them into `transport/`, `application/`, `domain/`, and `infrastructure/` subfolders.
7. **Avoid circular dependencies:** Features may rely on shared abstractions, but they should not depend directly on each other's internal implementation files.
8. **Compose from the root:** Wire routes or modules from a single app entry point that assembles features as units.
9. **Adapt the pattern, not the literal example:** Rename files, layers, contracts, and integrations to match the target project's architecture, framework conventions, and business language.

**Instrucciones (ES):**
1. **Hacer del dominio la primera regla de organización:** Crea una carpeta por área del negocio dentro de la raíz de código usando el estilo que encaje con el stack, por ejemplo `src/modules/`, `src/features/`, `app/domains/` o `internal/`.
2. **Modelar contextos delimitados, no dominios de demo:** Organiza el backend alrededor de áreas reales como `catalog`, `billing`, `identity`, `fulfillment`, `reporting` o `integrations`, no alrededor de ejemplos tutoriales.
3. **Mantener el flujo completo dentro del módulo:** Coloca el controlador o handler, el servicio o caso de uso, el repositorio, los DTOs, las entidades y las pruebas junto al mismo dominio para que la historia completa se lea en un solo lugar.
4. **Sacar solo lo realmente transversal:** Configuración, auth, logging, middleware, observabilidad, utilidades compartidas y bootstrap del framework van en `core/`, `shared/`, `common/` o su equivalente.
5. **Exponer un límite público:** Importa o registra cada feature mediante `index.{ext}`, `{domain}.module.{ext}`, exports de paquete o el equivalente del framework, en lugar de importar archivos internos en profundidad desde otro módulo.
6. **Permitir que la profundidad del módulo escale:** Un proyecto pequeño puede dejar `controller`, `service` y `repository` directo dentro del dominio. Uno más grande puede separarlos en `transport/`, `application/`, `domain/` e `infrastructure/`.
7. **Evitar dependencias circulares:** Los features pueden apoyarse en abstracciones compartidas, pero no deben depender directamente de archivos internos de implementación de otros módulos.
8. **Componer desde la raíz:** Registra rutas o módulos desde un único punto de entrada que ensamble los features como unidades.
9. **Adapta el patrón, no el ejemplo literal:** Renombra archivos, capas, contratos e integraciones para ajustarlos a la arquitectura, las convenciones del framework y el lenguaje de negocio del proyecto objetivo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @02-modular-project-structure to reorganize this backend by business domains.
1. Create one module per feature so each domain can be understood without opening unrelated folders.
2. Keep controller, service, repository, dto, entities and tests inside the same module, and move only cross-cutting code to common layers.
```

**Prompt (ES):**
```text
Usa la skill @02-modular-project-structure para reorganizar este backend por dominios del negocio.
1. Crea un módulo por feature para que cada dominio pueda entenderse sin abrir carpetas no relacionadas.
2. Deja controller, service, repository, dto, entidades y pruebas dentro del mismo módulo, y mueve solo lo transversal a capas comunes.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
├── app-entry.{ext}
├── core/
│   ├── config/
│   ├── auth/
│   ├── persistence/
│   └── observability/
├── shared/
│   ├── contracts/
│   ├── utils/
│   └── types/
└── {modules-root}/
    ├── {domain-a}/
    │   ├── transport/
    │   │   ├── {domain-a}.controller.{ext}
    │   │   └── dto/
    │   ├── application/
    │   │   └── {domain-a}.service.{ext}
    │   ├── domain/
    │   ├── infrastructure/
    │   │   └── {domain-a}.repository.{ext}
    │   ├── index.{ext} or {domain-a}.module.{ext}
    │   └── tests/
    └── {domain-b}/
        └── ...
```

Read [resources/module-structure.template.md](resources/module-structure.template.md) when you need a scaffold for one module, and [resources/naming-conventions.md](resources/naming-conventions.md) when adapting the pattern to a specific language or framework.

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Each feature can be understood without opening unrelated folders.
- [ ] Files used by only one business domain live inside that domain module.
- [ ] Cross-cutting concerns live outside the feature modules.
- [ ] Other features import only the module public entrypoint, not its internal files.
- [ ] Names, files, layers, and integrations were adapted to the target project's conventions instead of copying the example structure literally.

**Checklist (ES):**
- [ ] Cada feature puede entenderse sin abrir carpetas no relacionadas.
- [ ] Los archivos que pertenecen a un solo dominio viven dentro de ese módulo.
- [ ] Las preocupaciones transversales viven fuera de los módulos de dominio.
- [ ] Los demás features importan solo el punto de entrada público del módulo, no sus archivos internos.
- [ ] Los nombres, archivos, capas e integraciones se adaptaron a las convenciones del proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
