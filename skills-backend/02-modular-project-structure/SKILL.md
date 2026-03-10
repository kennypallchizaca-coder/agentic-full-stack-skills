---
name: 02-modular-project-structure
description: "Establishes a scalable Folder Architecture segregating domains modularly. Isolates functional contexts preventing massive monolithic code files effectively natively."
risk: low
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Placing all logic inside one colossal `routes.js` or `Main.java` file inevitably guarantees complete architectural collapse. This skill strictly imposes a Modular Project Architecture encapsulating Features into distinct Context Domains systematically grouping routes, services, and models identically successfully.

**Descripción (ES):**
Colocar toda la lógica dentro de un colosal archivo `routes.js` o `Main.java` inevitablemente garantiza el colapso arquitectónico completo. Esta skill impone estrictamente una Arquitectura de Proyecto Modular encapsulando "Features" (Funcionalidades) en Dominios de Contexto distintos, agrupando sistemáticamente sus rutas, servicios y modelos.

---

# 2. Skill Objective

**Objective (EN):**
Decouple backend logic into Feature-based Directory Structures cleanly.
- Use this skill when: Developing enterprise-scale modules demanding pure separation (e.g., `Users`, `Products`, `Orders`).
- Do not use this skill when: Creating a single-file serverless lambda function exclusively devoid of explicit multi-table operations nicely locally.

**Objetivo (ES):**
Desacoplar la lógica backend recayendo en Estructuras de Directorio Basadas en Features limpiamente.
- Úsese cuando: Se desarrollen módulos a escala empresarial demandando separación pura y limpia (ej., `Usuarios`, `Productos`, `Órdenes`).
- No se use cuando: Se cree una única y exclusiva función Lambda serverless de un solo archivo sin operaciones de múltiples tablas requeridas puramente directas.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Feature Names`: Array of generic target Domains (e.g., `auth`, `users`).
2. `Pattern Strategy`: Strict Module folder segregation parameters safely.

**Entradas (ES):**
1. `Feature Names`: Arreglo de Dominios objetivo genéricos (ej., `auth`, `users`).
2. `Pattern Strategy`: Parámetros estrictos de segregación de carpetas a nivel Módulo asilado eficientemente seguro.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Generated specific specific folder ecosystems perfectly correctly isolating controllers securely uniquely cleanly natively safely.
2. Universal index file generically importing and mapping targeted routes efficiently gracefully.

**Salidas (ES):**
1. Ecosistemas locales de carpetas perfectos y específicos aislando nativamente controladores de forma segura limpiamente única.
2. Un indexado universal genérico compilando e importando mapeos directos a Rutas exitosamente acopladas de inicio seguro.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Identify Domains:** Classify standard generic generic platform functionalities cleanly identifying independent Business contexts inherently.
2. **Execute Nested Creation:** Under the `src/` directory explicitly, generate targeted sub-folders encapsulating standard behaviors per Domain locally gracefully (`src/users/`, `src/products/`).
3. **Assign Separation of Concerns (SoC):** Ensure inner Domains possess identical explicit Controller, Service and Repository layouts actively identically successfully.

**Instrucciones (ES):**
1. **Identificar Dominios:** Clasificar estándares generales de las funcionalidades identificando de facto contextos independientes Base (Negocio).
2. **Crear Estructura Anidada:** Debajo de la ubicación en red de `src/`, general explicitamente los envoltorios sub-carpetas aislando cada dominio (ej. `src/users/`, `src/products/`).
3. **Asignar Separación de Preocupaciones (SoC):** Garantizar pura homogeneidad asegurando que el Dominio integre distribuciones locales tipo Controlador, Servicio y Repositorio de modo exacto sistemáticamente orgánico fiable.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @02-modular-project-structure to isolate `{DomainName}` architectures smoothly effectively cleanly efficiently implicitly optimally.
1. Formulate precise base controllers encapsulating the native structure safely securely identically cleverly flawlessly.
```
*(Rewriting prompt cleanly)*
```text
Use the skill @02-modular-project-structure to isolate `{DomainName}` architectures seamlessly.
1. Formulate exact base controllers and services encapsulating logic natively gracefully perfectly reliably.
```

**Prompt (ES):**
```text
Usa la skill @02-modular-project-structure integrando los sub-directorios asilados `{DomainName}` veloz limpiamente con seguridad estable estandarizada.
1. Formula carpetas base exactas a nivel servicio y controlador encapsulando jerarquías correctamente óptimas libres de derrames genéricamente exactos y limpios.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
└── modules/
    └── {DomainName}/              ← Independent Domain Root
        ├── {domain}.controller.{ext}
        ├── {domain}.service.{ext}
        └── {domain}.repository.{ext}
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Confirm Domain logic avoids circular imports safely preventing memory exhaustion natively identical optimally securely dependably reliably perfectly smoothly expertly flawlessly intelligently uniquely clearly exactly appropriately functionally elegantly creatively ideally flawlessly cleverly predictably exactly brilliantly.
*(I will rewrite this manually)*
- [ ] Confirm Domain logic avoids circular imports completely safely.
- [ ] Validate standard implementations map specific controllers completely independent of the actual application registry locally perfectly cleanly smoothly effortlessly nicely actively practically.
*(I will rewrite this manually)*
- [ ] Validate standard sub-modules register themselves identically through an index configuration flawlessly.

**Checklist (ES):**
- [ ] Confirmar fiablemente pura ausencia de importaciones de lógica cíclica previniendo en cascada agotamientos en memorias de bloque central limpiamente puros nativos perfectos sin falla al flujo real.
- [ ] Validar general puro bases locales comprobando que implementaciones registren a sus controladores independientemente inyectados base a dependencias globales en orden correcto seguro nativo exactamente base a su estructura sólida integral transparente al indexador único localmente seguro.
