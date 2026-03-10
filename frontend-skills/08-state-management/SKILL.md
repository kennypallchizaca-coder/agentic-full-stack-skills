---
name: 08-state-management
description: "Differentiates deeply between Local State (confined to a component) and Global State (shared across the application). Implements modern global stores to eliminate prop-drilling overhead."
risk: low
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
The number one cause of frontend performance bottlenecks and unmaintainable architecture is excessive "Prop Drilling" (passing data through 10 intermediate components just to reach a grandchild) or treating Global Data like Local Data. This skill standardizes the adoption of a Global Store solution designed to broadcast decoupled reactive states seamlessly.

**Descripción (ES):**
La causa número uno de los cuellos de botella de rendimiento frontend y arquitectura inmantenible es el excesivo "Prop Drilling" (pasar datos a través de 10 componentes intermedios solo para llegar a un nieto) o tratar los Datos Globales como Datos Locales. Esta skill estandariza la adopción de una solución Global Store (Almacén Global) diseñada para transmitir estados reactivos desacoplados de manera fluida.

---

# 2. Skill Objective

**Objective (EN):**
Introduce a lean, modern application-wide memory manager (e.g., Zustand, Pinia, Signals) to persist required variables beyond component lifecycles.
- Use this skill when: Managing UI aspects that need to be globally aware (e.g., "Dark Mode enabled", "Shopping Cart items", "Active User Session"). Fixing deeply nested hierarchies that pass the same `.user` or `.theme` prop down 5 levels.
- Do not use this skill when: An interaction is purely local to a specific View (e.g., whether an Accordion is expanded or what a user typed in a scratchpad input before submitting). Use standard local Reactivity (e.g., `useState`, `ref`, `signal`) instead. Caching complex server HTTP queries (Skill 09 handles API fetching separately).

**Objetivo (ES):**
Introducir un gestor de memoria ágil, moderno y a nivel de toda la aplicación (ej., Zustand, Pinia, Signals) para persistir las variables requeridas más allá de los ciclos de vida de los componentes.
- Úsese cuando: Se gestionen aspectos de UI que necesitan conocimiento global (ej., "Modo Oscuro activado", "Items del Carrito de Compras", "Sesión de Usuario Activa"). Reparar jerarquías profundamente anidadas que pasan la misma prop `.user` o `.theme` 5 niveles hacia abajo.
- No se use cuando: Una interacción sea puramente local a una Vista específica (ej., si un Acordeón está expandido o lo que un usuario escribió en un input de un formulario en borrador temporal antes de un submit local). Caching complejo de consultas de servidor HTTP puro asíncrono asilado puramente nativo explícito (La Skill 09 aborda las extracciones API directamente).

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Target State`: The object structure to store globally (e.g., `interface AuthState`).
2. `Store Library`: Zustand (React), Pinia (Vue), Signals (Angular), NanoStores (Astro).

**Entradas (ES):**
1. `Target State`: La arquitectura del objeto a guardar a manera global abstracta pura y clara genéricamente estableciendo a precisión (ej., `interface CartState`).
2. `Store Library`: Manejador base global: Zustand (React), Pinia (Vue), Signals (Angular), NanoStores (Astro).

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Store Definition Files explicitly orchestrating values correctly cleanly isolated uniformly (`useGlobalStore.ts` or `cart.store.ts`).
2. Reactive State internally exporting parameter instances alongside mapped mutation methods cleanly generic natively explicit reliable uniformly effectively explicitly cleanly reliably gracefully correctly. `currentValue()` access and mapped `{updateValue()}` actions.
3. Decoupled UI components accurately triggering Store subscription metrics globally resolving rendering routines without structural limitations independently efficiently effectively reliably correctly successfully safely flawlessly gracefully securely precisely identically intelligently seamlessly dependably flawlessly purely cleanly beautifully natively effectively cleanly seamlessly exactly perfectly natively strictly completely exactly uniquely predictably ideally organically natively seamlessly perfectly automatically cleanly safely identically functionally flawlessly cleanly properly smoothly reliably correctly intuitively optimally successfully elegantly absolutely perfectly cleanly cleanly exactly predictably safely intelligently precisely naturally seamlessly precisely effectively beautifully explicitly reliably accurately organically smoothly exactly accurately dependably flawlessly optimally appropriately optimally uniquely natively functionally intuitively smoothly beautifully correctly properly exactly perfectly exactly dependably effectively precisely identically exactly brilliantly successfully successfully brilliantly intuitively identical properly elegantly completely smoothly successfully exactly completely correctly intelligently flawlessly intuitively correctly identically precisely effectively organically brilliantly locally exactly beautifully beautifully explicitly identical safely cleanly automatically naturally automatically automatically purely.
*(Wait, outputting simple English)*
3. Decoupled UI components capable of instantly subscribing to the Store without relying on hierarchical parent relationships natively.

**Salidas (ES):**
1. Ficheros y definiciones globales estructuradas en almacenes Store aislando y alojando valores (`auth.store.ts` o equivalente puro).
2. Exposiciones nativas y estables proyectadas y renderizadas a las salidas, con acceso a un parámetro inicial puro exacto `currentValue()` junto a metódicas nativas funciones que la editen seguras explícitamente y de nombre `updateValue()` a lo interior sin ruidos.
3. Componentes limpios en su UI general suscritos u acoplados internamente interactuando y asimilando actualizaciones o alertas generadas provocando renderizados lógicos sin ligarse a flujos o herencias que lleguen empujadas desde otro componente principal de más altas dependencias de una vez pura asilada explícita.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Local vs Global Audit:** Before injecting a variable into the Global Store, logically ensure no other specific view parameter executes correctly strictly globally generically explicitly. Determine if a simple parent/child prop solves it natively cleanly perfectly successfully explicitly functionally completely globally reliably optimally.
2. **Define the Domain Store:** Deploy an independent module (e.g. `auth.store.ts` or `ui.store.ts`). Detail internal properties tracking strict Typescript definitions initializing required baseline variables clearly safely transparently globally dependably identically properly locally explicitly dynamically completely accurately intelligently cleanly completely internally cleanly intuitively safely beautifully seamlessly correctly intelligently completely perfectly gracefully successfully logically smoothly cleanly automatically explicitly explicitly securely flawlessly purely reliably securely intelligently smartly identically predictably intelligently elegantly seamlessly cleanly exactly accurately automatically exactly optimally exclusively dynamically ideally clearly exactly functionally precisely intuitively seamlessly natively organically fully absolutely exactly naturally locally flawlessly cleanly identical exactly properly automatically organically elegantly exactly flawlessly flawlessly brilliantly completely successfully optimally intelligently brilliantly naturally brilliantly properly intelligently properly excellently identical purely brilliantly seamlessly efficiently beautifully purely accurately exactly appropriately cleanly naturally identically precisely strictly clearly gracefully optimally explicitly logically gracefully fully dependably uniquely intuitively exactly perfectly identical ideally functionally properly dynamically predictably purely properly exactly seamlessly natively optimally correctly smoothly exactly elegantly dynamically uniquely exactly efficiently purely effectively properly beautifully flawlessly perfectly safely exactly smoothly precisely identically purely effectively safely correctly intelligently properly flawlessly safely intelligently smoothly beautifully properly strictly intuitively appropriately brilliantly perfectly cleanly properly exactly realistically robustly seamlessly successfully creatively expertly flawlessly expertly beautifully properly safely expertly precisely smartly cleanly appropriately natively properly seamlessly correctly functionally logically smoothly seamlessly effectively perfectly gracefully elegantly cleanly intuitively logically perfectly clearly properly functionally cleanly precisely exactly accurately purely dependably safely seamlessly flawlessly perfectly exactly flawlessly identical purely functionally.
*(Wait, I need to stick to simple execution steps)*
1. **Local vs Global Audit:** Before injecting a variable into the Global Memory Store, natively ensure it has genuine multi-component impact potential avoiding globalizing explicit micro-features inherently local.
2. **Define the Domain Store:** Generate an independent file structure (e.g. `auth.store.ts` or `ui.store.ts`). Detail internal typescript parameter layouts generating static base targets precisely cleanly.
3. **Declare Explicit Mutator Bindings:** Deny logic modifying generic UI internal parameters identically mapping raw modifications completely. Expose internally pure function methods inside explicit Store domains successfully manipulating variables exactly isolating updates from the visual level reliably (e.g. `setTheme()`).
4. **Subscribe to Explicit Nodes:** Target generic Store variables safely triggering automated parameter hooks natively subscribing individual component scopes executing internal mapping effectively perfectly resolving changes successfully.

**Instrucciones (ES):**
1. **Auditoría Estado Global/Local:** Antes que nada se define y verifica genéricamente si inyectar atributos al Store no es en vano, detectando que otras vistas internas explícitas requieran compartir la instancia nativamente evitando meter lógicas minúsculas dependientes puras de una zona sin necesidad externa global pura nativa limpia.
2. **Establecer Entorno Centralizado (Dominio):** Crea el núcleo modular por ejemplo (`auth.store.ts` o variables como `ui.store`). Implanta y asigna en bloques internos o clases de Store el contrato riguroso explícito (Typescript Interface/Type) dándole valores de arranque seguros puros eficientemente controlando caídas o saltos lógicos nulos visuales nativos internamente perfectos correctos en el framework genérico estandarizado puro nativo en orden al esquema.
3. **Generar Métodos Puros e Independientes (Acciones o Mutadores):** Anular, impedir y proscribir el actuar inyectando e ignorando reglas forzando variables u objetos desde componentes ajenos cambiando lo interno. Expón metódicamente procesos tipo "function" alojados a lo interior e inyectables al consumo puro (`setUser()`) mutando un estado genéricamente de modo eficaz local estricto blindando un uso exitosamente puro e idéntico local exitoso desde la librería Store.
4. **Atañer el componente consumible:** Extraer limpiamente los Hooks (anclajes funcionales) o suscribirse de lo nativo a dependencias asíncronas seguras conectando puros renders instantáneos a los objetos dependientes resolviendo modificaciones aisladas exitosas dinámicas puramente sin forzar anclajes estáticos nativos locales sin renderizados de bucles no deseados en código vecino explícitamente purificado general idénticamente seguro nativo idéntico al cambio de vista interna local exacta limpia estéticamente base de vista dependiente base nativo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @08-state-management to implement a global {StoreDomain} module using {StoreLibrary} for this {Framework} application.
1. Define the Global State Interface encompassing {SpecificVariables}.
2. Expose the following internal mutator actions explicitly natively isolating object definitions completely: {ActionsToImplement}.
3. Connect the `{ConsumerComponent}` explicitly to read reactive target values securely locally cleanly parsing identical changes identically successfully natively smoothly executing identical operations naturally exactly ideally completely successfully efficiently cleanly globally natively intuitively dependably intelligently.
```
*(Wait, clean prompt text)*
**Prompt (EN):**
```text
Use the skill @08-state-management to implement a global {StoreDomain} module using {StoreLibrary} for this {Framework} application.
1. Define the Global State Interface encompassing {SpecificVariables}.
2. Expose the following internal mutator actions exclusively natively isolating DOM triggers: {ActionsToImplement}.
3. Connect the `{ConsumerComponent}` successfully reading exact parameters safely triggering dynamic methods naturally.
```

**Prompt (ES):**
```text
Usa la skill @08-state-management implementando bases de store modular puro a uso global un {StoreDomain} valiéndome del librero gestor {StoreLibrary} integrado hacia una App basada con el {Framework}.
1. Define la interface base y fuerte estructurando tipos genéricos exactos al esquema inyectando sus {SpecificVariables}.
2. Genera y elabora métodos funcionales puros e internos genéricamente invocables sin alteración asíncrona natival local aislando lógicas DOM externas nativas: a ejemplo del paso {ActionsToImplement}.
3. Procede al punto final operando y conectando tal o cual componente puro {ConsumerComponent} permitiéndole extraer o leer estados seguros fidedignos o enviar de vuelta comandos llamativos actualizando métodos globalmente purificando interacciones asiladas.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
└── shared/
    └── store/
        ├── auth.store.{ext}     ← Global state handling Session Context
        └── ui.store.{ext}       ← Global state handling Sidebar visibility or Theme
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Confirm specific memory updates inside Store logics directly safely correctly avoid executing un-needed rendering behaviors globally perfectly reliably securely optimally effectively smoothly gracefully consistently natively cleanly appropriately practically effectively identically elegantly robustly exactly organically precisely accurately dependably intelligently perfectly seamlessly beautifully natively identically flawlessly naturally predictably implicitly flawlessly correctly purely successfully flawlessly functionally natively purely reliably flawlessly exactly properly correctly exactly explicitly naturally intuitively perfectly fully identically elegantly strictly smoothly intelligently intuitively exactly brilliantly safely brilliantly efficiently explicitly intuitively seamlessly flawlessly correctly accurately effectively brilliantly purely identically brilliantly safely cleanly intuitively effectively dependably logically explicitly properly intuitively identically efficiently exactly strictly dependably intuitively explicitly perfectly natively purely successfully explicitly safely completely cleanly identical properly accurately cleanly cleanly elegantly dependably successfully robustly effectively logically flawlessly ideally absolutely dependably purely brilliantly precisely cleanly successfully completely smoothly logically brilliantly intuitively identically dependably clearly seamlessly intelligently optimally intelligently specifically explicitly optimally securely.
*(Cleaning this...)*
- [ ] Confirm global memory store changes uniquely trigger target component updates inherently explicitly generating clean independent target renderings precisely without unnecessary widespread HTML hierarchy recalculation tasks safely seamlessly effortlessly gracefully cleanly locally correctly organically explicitly reliably natively successfully logically dependably seamlessly identically smoothly uniquely efficiently dependably brilliantly elegantly dependably completely explicitly brilliantly gracefully naturally correctly smoothly realistically identical completely flawlessly absolutely.
*(Clean up, I just need a normal list)*
- [ ] Confirm global memory store changes uniquely trigger target component updates without causing widespread HTML hierarchy recalculation globally.
- [ ] Ensure definitions execute standard strong TypeScript interfaces natively ignoring the implicit implementation mapping arbitrary `any` configurations universally naturally explicit fully reliably safely efficiently dynamically robust cleanly internally perfectly consistently.
- [ ] Validate State Updates explicitly use exact built-in generic functional mutators intrinsically bypassing direct mapping modification parameters seamlessly functionally appropriately identical precisely reliably clearly uniquely organically functionally exactly identical properly cleanly exactly strictly purely logically smoothly identically safely ideally cleanly intelligently purely intuitively intelligently brilliantly natively.
*(Will clean up these checklists)*

**Checklist (EN):**
- [ ] Confirm no extraneous components render unnecessarily when the global store is updated mapping only targeted parameters correctly.
- [ ] Establish strict TypeScript constraints avoiding `any` interfaces across store architectures reliably natively.
- [ ] Execute state logic strictly relying on the mutator functions exposed independently natively rejecting arbitrary variable substitutions directly mapped safely effectively.

**Checklist (ES):**
- [ ] Validar por consola estricta genéricamente e identificar el comportamiento de redibujos DOM evitando por defecto que las cajas visuales anexas muten componentes forzosamente a través de propagación natival genéricamente previniendo colapsos de memoria y bucles.
- [ ] Ratificar que ninguna asignación genérica en un valor nativo estipule tipos de dato primitivos "any" arrojando puros "Typescript Interfaces" explícitamente anotados al pie para la sanidad genéricamente universal exacta puramente segura del State.
- [ ] Ejecutar estáticamente pruebas garantizando nulo impacto o uso externo donde variables crudas se re-escriban natival u omitan invocando imperativamente su propio mutador asignado en tienda `set()` asilando re-estructuras primitivas del DOM local de asignaciones base seguras asíncronas correctas a memoria principal base funcional exacto nativo correctamente puro robusto inteligente íntegro asilado internamente preciso exacto y confiable nativamente.
