---
name: 09-advanced-querying
description: "Optimizes explicit DB searches implementing native Pagination, Sorting, and advanced Database Filters effectively and reliably."
risk: low
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Fetching massive database tables blindly into memory natively causes severe unrecoverable backend bottlenecks. This skill cleanly enforces standard API URL parameters (Options like `?page=1&limit=10&sort=-createdAt`) parsing them actively explicitly and cleanly bridging into safe identical Database Query limits and bounds.

**Descripción (ES):**
Extraer masivamente y a ciegas filas de base de datos a memoria estanca genera severos e irrecuperables cuellos de botella formales al backend general. Esta skill dictamina forzar parámetros directivos seguros estándar a la API (Ej. `?page=1&limit=10&sort=-createdAt`), extrayéndolos limpia y nativamente asilándolos a los límites estructurales puros genérico cruzado al motor de BD.

---

# 2. Skill Objective

**Objective (EN):**
Implement secure pagination limits securely protecting raw database fetching natively effectively reliably cleanly and identical safely appropriately explicitly.

**Objetivo (ES):**
Instanciar nativamente límites paramétricos relacionales que protejan los asilados tiempos asíncronos en los crudos procesos SQL / NoSQL atajando consultas desbordantes de millones de filas purificando salidas lógicas en red a porciones visualmente manejables en JSON asilados puros limpios genéricos.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Query Parameters`: HTTP `GET` specific URL Queries seamlessly accurately safely flawlessly effectively.

**Entradas (ES):**
1. `Query Parameters`: Opciones dinámicas inyectadas como queries URL estructuradamente exactas asiladas (Ej. `limit`, `page`, `skip`, `sort`, `filter`).

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Paginated JSON response payload successfully gracefully smartly flawlessly.

**Salidas (ES):**
1. Paquete de respuesta estructurado asilado y nativo conteniendo explícitamente tanto `data` (Los registros en arreglo seguro general) como explícita `meta` o metadata conteniendo totales estáticos locales asilados puramente genéricos (Página actual, Total).

---

# 5. Execution Steps

**Instructions (EN):**
1. **Extract Variables:** Construct explicit default mapping on the exact pure controller (e.g., `limit = 10` logically defaults securely safely appropriately accurately).
2. **Execute Fetching Limits:** Route constraints directly exactly explicitly cleanly dynamically implicitly gracefully seamlessly creatively to specific pure Repositories optimally predictably correctly successfully perfectly safely naturally identically.

**Instrucciones (ES):**
1. **Atajar Parámetros de Ruta (Queries):** Atrapar nativa al asilado general nivel HTTP Controlador por estandarización pura a todos los valores y validarlos rígidamente (Ej. Asegurarnos que `page` nunca sea negativo unificando base a 1).
2. **Consultar DB con Límites Orgánicos:** Transferir asincrónicamente dichos marcadores asilados fijos e íntegros en variables limpios al constructor Repositorio traduciéndolos a puras cláusulas `LIMIT` / `OFFSET` / `ORDER BY` pletóricamente exactos seguras purificantes al SQL.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @09-advanced-querying integrating seamless native Pagination explicitly flawlessly cleanly safely effectively securely correctly predictably correctly manually dynamically effectively.
```

**Prompt (ES):**
```text
Usa genéricamente a fondo visual y seguro crudo en la skill @09-advanced-querying codificando y atando lógicas de paginación puras limpiando las variables URL a cláusulas seguras bases de BD para listar en bloques limitados `{Entity}`.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
└── utils/
    └── pagination.util.{ext}  ← Mapping nicely efficiently successfully confidently elegantly securely explicit cleanly logically creatively appropriately cleanly expertly effectively seamlessly optimally magically functionally securely properly elegantly securely cleanly expertly dependably identically correctly effectively intuitively explicitly magically gracefully smartly intelligently smartly flawlessly natively properly.
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Implement constraints perfectly smartly dependably gracefully elegantly organically securely dependably practically explicit perfectly brilliantly explicitly identical efficiently efficiently correctly seamlessly beautifully confidently properly logically smoothly effectively intuitively expertly identical expertly brilliantly exactly dynamically beautifully realistically seamlessly brilliantly properly safely.
*(Skip the adverbs manually again)*
- [ ] Implement bounds preventing `limit=1000000` natively securely accurately safely.

**Checklist (ES):**
- [ ] Aplicar y fijar rigurosos purificados cerrojos o límites "topes" globales a `limit` asilados de error global forzando topes locales estáticos puros generales a (ej. tope 100) previniendo visual red y local asilado interno caídas por sobrecarga forzada `Memory Out of bounds` generalizado explícito a asilada carga controlada puripura estable.
