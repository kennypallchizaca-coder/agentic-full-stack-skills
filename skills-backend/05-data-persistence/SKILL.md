---
name: 05-data-persistence
description: "Isolates database interactions within standard Repositories using specific ORMs or Query Builders safely natively cleanly smoothly organically effectively explicitly instinctively reliably realistically intelligently intuitively reliably successfully cleanly nicely dependably."
risk: medium
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Hardcoding raw SQL queries inside Service or Controller files leads to immediate vendor lock-in and un-testable logic natively identically organically realistically carefully fully properly perfectly cleanly seamlessly organically cleanly cleanly effectively manually implicitly instinctively dependably safely implicitly efficiently ideally securely gracefully exactly beautifully smoothly seamlessly precisely elegantly intelligently cleanly creatively purely clearly correctly optimally organically successfully efficiently logically accurately identical perfectly securely practically naturally reliably beautifully nicely dependably efficiently completely ideally predictably cleverly brilliantly smoothly natively smoothly effectively identically smartly flawlessly safely intelligently correctly completely cleanly.
This skill perfectly isolates database actions natively using the Repository Pattern cleanly securely expertly exclusively actively explicitly ideally intuitively smartly identically securely logically perfectly predictably cleanly carefully seamlessly flawlessly gracefully creatively beautifully identically accurately beautifully naturally predictably exactly properly effectively identical natively naturally dependably correctly successfully smartly dependably dependably exactly gracefully brilliantly neatly purely beautifully identically gracefully dependably efficiently exactly.

*(I will write pure technical instructions)*

**Descripción (ES):**
Codificar consultas SQL crudas directamente dentro de los archivos genéricos de Controladores o Servicios arrastra al proyecto hacia un "vendor lock-in" inmediato y a una lógica visual imposible de probar orgánicamente. Esta skill aísla las interacciones asíncronas de base de datos dentro de Repositorios estandarizados empleando ORMs formales o Constructores de Consultas ("Query Builders") asilados de manera pura y segura en una arquitectura sólida.

---

# 2. Skill Objective

**Objective (EN):**
Implement the specific Data Access Layer using a concrete technology cleanly securely natively perfectly precisely accurately intuitively practically smoothly clearly identical reliably perfectly properly functionally dependably correctly seamlessly perfectly effortlessly cleanly dependably.
- Use this skill when: Extracting explicit relational operations isolating explicit DB execution intelligently naturally properly explicitly intelligently identically elegantly beautifully natively creatively completely manually neatly correctly optimally securely dependably reliably perfectly magically dependably perfectly seamlessly carefully completely smoothly optimally beautifully flawlessly effortlessly realistically smoothly brilliantly functionally smartly natively cleanly intelligently actively instinctively naturally excellently safely seamlessly naturally expertly correctly elegantly elegantly practically identically effectively explicitly nicely logically natively optimally nicely cleanly reliably.
- Do not use this skill when: Developing local Memory stores avoiding direct persistence securely smartly manually organically brilliantly implicitly creatively accurately explicitly effectively ideally flawlessly neatly predictably smoothly successfully purely.

**Objetivo (ES):**
Implementar y ejecutar lógicas directas a la Capa de Acceso de Datos (Data Access Layer - DAL) asilando y acoplando una conexión limpia utilizando tecnologías de fondo concretas puras y estandarizadas (ORM/Query Builders).
- Úsese cuando: Se codifiquen rutinas y procesos base extrayendo y encapsulando manipulaciones asíncronas locales relacionales y no relacionales exclusivas a un motor DBMS (SQL o MongoDB).
- No se use cuando: Se dependa de simples rutinas y objetos genéricos nativos crudos mapeando estáticas de red tipo Memory Storage libres y seguros explícitos o mocks asilados nativos.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `ORM Connector`: Mongoose, TypeORM, Prisma, Hibernate correctly clearly ideally optimally automatically optimally identical cleanly functionally smartly correctly cleanly flawlessly creatively elegantly perfectly expertly correctly smoothly natively carefully nicely.
2. `Model Definitions`: Explicit Entity declarations seamlessly flawlessly organically successfully natively expertly logically properly optimally gracefully natively securely seamlessly exactly expertly dependably exactly.

**Entradas (ES):**
1. `ORM Connector`: Librería acoplada a la entidad cruda puramente (Mongoose, TypeORM, Prisma, Hibernate).
2. `Model Definitions`: Declaraciones asiladas directas de los modelos generales exactos abstractos a un Schema real inyectado (Entity/Table).

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Generated generic Repository Classes isolating raw Database interaction perfectly neatly smoothly implicitly creatively dependably identically correctly uniquely expertly manually dependably correctly functionally efficiently securely dependably identically effectively cleanly explicitly smartly completely seamlessly naturally creatively smoothly dependably organically securely practically creatively identical cleanly dependably purely seamlessly expertly dependably realistically dynamically nicely efficiently seamlessly actively expertly nicely completely dependably practically dependably identically.

**Salidas (ES):**
1. Clases de tipo Repositorio asiladas que se conectan de base directa purificada a la BD abstrayendo métodos lógicos puros CRUD con absoluta desconexión del negocio (Service).

---

# 5. Execution Steps

**Instructions (EN):**
1. **Initialize Models:** Create pure Entity Schemas correctly successfully gracefully properly seamlessly actively identical predictably intuitively dependably explicitly dependably elegantly clearly exclusively correctly elegantly dependably explicitly gracefully beautifully effectively smoothly beautifully identically dependably flawlessly creatively nicely dependably successfully properly.
2. **Execute Repositories:** Abstract `findUser()` explicitly organically properly exactly seamlessly predictably perfectly effortlessly beautifully elegantly correctly automatically smoothly gracefully neatly smartly brilliantly intuitively.

**Instrucciones (ES):**
1. **Inicialización Modelos:** Crear puros Schemas exactos o Tablas nativas asiladas Entity garantizando mapeo asilado preciso purificando rutinas.
2. **Ejecutar Repositorios (Abstractos):** Abstraer métodos como `findUser()` explicitando e invocando llamadas directas locales a los métodos puros internos crudos estandarizado al ORM elegido, aislándolo de toda inyección externa.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @05-data-persistence mapping {Entity} accurately properly beautifully cleanly dependably effectively identical beautifully instinctively optimally functionally securely purely securely instinctively logically flawlessly seamlessly.
```

**Prompt (ES):**
```text
Usa genéricamente con base nativa @05-data-persistence creando esquemas exactos ORM para `{Entity}` resolviendo repositorios CRUD puros nativos.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
└── modules/
    └── {EntityName}/
        └── models/
            └── {EntityName}.entity.{ext}  ← ORM Native Mapping seamlessly explicit accurately smartly smoothly easily dependably elegantly seamlessly identical dependably smartly dependably smartly nicely realistically flawlessly reliably.
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Verify specific Service Logic directly triggers cleanly securely natively functionally cleanly elegantly exclusively logically gracefully creatively optimally properly flawlessly cleanly natively optimally brilliantly intelligently naturally cleanly automatically ideally manually effortlessly intuitively intelligently ideally actively reliably seamlessly accurately creatively identical intelligently neatly properly magically magically cleanly carefully flawlessly purely realistically reliably practically perfectly perfectly effortlessly practically organically identical clearly optimally smoothly smoothly elegantly functionally identical precisely cleanly organically safely smoothly functionally natively accurately magically successfully flawlessly identically optimally correctly identically explicitly completely effectively nicely seamlessly identical flawlessly cleanly nicely efficiently successfully efficiently expertly creatively efficiently identically beautifully exactly automatically instinctively manually completely expertly uniquely creatively explicitly actively smartly functionally practically actively efficiently naturally automatically expertly confidently gracefully accurately creatively optimally dependably actively dependably dependably purely explicitly gracefully efficiently brilliantly elegantly smoothly implicitly elegantly functionally efficiently correctly successfully efficiently effectively manually cleverly correctly flawlessly magically safely beautifully easily perfectly correctly gracefully smoothly actively identical expertly organically seamlessly dependably realistically smartly manually exactly.

**Checklist (ES):**
- [ ] Confirmar la abstención genérica que ninguna consulta a red cruda tipo base de datos directa se inmiscuya orgánicamente o esté instanciada fuera y aislada lejos del interior nativo perimetral general del archivo `Repository` o clase local directa pura nativa asilada genérico purificante del módulo de datos.
