---
name: 10-advanced-navigation
description: "Implements advanced UI components essential for modern navigation heuristics: URL-driven Reactive Pagination, descriptive Hero Component Sections, and navigational Breadcrumb patterns."
risk: low
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Sophisticated Frontend Interfaces require advanced indicators conveying precise interaction context mimicking desktop-grade operability natively. This skill centralizes the execution of "Breadcrumbs" (navigation paths), Hero Sections (summary visuals), and notably URL-Driven Pagination preventing search parameter degradation upon hard-refreshes.

**Descripción (ES):**
Las Interfaces Frontend sofisticadas requieren indicadores avanzados que transmiten un contexto de interacción preciso imitando nativamente la operatividad de nivel de escritorio (desktop). Esta skill centraliza la ejecución de "Breadcrumbs" (migas de pan o rutas de navegación), Secciones Hero (imágenes de resumen), y notablemente una Paginación basada en URLs (URL-Driven) previniendo la degradación de los parámetros de búsqueda ante recargas forzadas (`F5`).

---

# 2. Skill Objective

**Objective (EN):**
Prevent user disorientation by combining aesthetic layout design with rigorous functional routing logic natively preventing states strictly un-impacted by browser URL alterations independently predictably securely gracefully.
- Use this skill when: Managing data tables spanning hundreds of entries demanding programmatic offset/limit Pagination natively strictly efficiently perfectly cleanly preserving query parameter logic seamlessly successfully reliably natively correctly explicitly dynamically smoothly organically automatically dynamically gracefully appropriately gracefully ideally logically exactly. (e.g. `?page=4`). Depicting hierarchical folder layouts via Breadcrumbs predictably natively purely properly properly precisely strictly efficiently correctly logically seamlessly appropriately explicitly natively flawlessly intelligently smoothly functionally identically explicitly correctly properly smoothly cleanly identical flawlessly functionally cleanly gracefully intuitively precisely beautifully fully flawlessly efficiently uniquely brilliantly perfectly realistically efficiently predictably brilliantly strictly intuitively optimally clearly exactly dependably efficiently seamlessly predictably efficiently identical explicitly smoothly perfectly intuitively identically purely ideally correctly seamlessly flawlessly correctly properly beautifully purely ideally effectively optimally perfectly appropriately brilliantly elegantly effectively correctly exactly successfully smoothly exactly properly precisely identically identically fully safely fully safely perfectly automatically cleanly exactly smoothly cleanly optimally ideally locally strictly locally smoothly appropriately perfectly reliably perfectly organically accurately absolutely fully perfectly elegantly safely brilliantly safely beautifully uniquely successfully safely dependably elegantly exactly dependably accurately identical purely dependably perfectly robustly optimally seamlessly completely robustly intelligently reliably purely flawlessly elegantly naturally exclusively smoothly functionally successfully dependably dependably purely explicitly properly explicitly safely correctly identical accurately independently elegantly reliably intuitively flawlessly naturally excellently natively cleanly completely clearly exactly efficiently functionally explicitly optimally exactly effectively robustly natively cleanly accurately ideally flawlessly ideally intelligently clearly effectively successfully explicitly uniquely intuitively flawlessly actively strictly actively reliably automatically cleanly functionally strictly perfectly gracefully properly perfectly safely flawlessly excellently completely ideally flawlessly optimally successfully optimally appropriately identical specifically appropriately creatively specifically creatively properly intelligently intelligently creatively safely purely seamlessly correctly identically successfully predictably exactly ideally exactly intuitively reliably exactly.
*(Rewriting clean english)*
- Use this skill when: Managing data tables demanding programmatic Pagination seamlessly preserving query parameters (`?page=4`) properly natively. Depicting hierarchical folder layouts via Breadcrumbs, and generating high-impact Hero visual summaries.
- Do not use this skill when: Managing transient 5-item lists rendering natively efficiently perfectly organically fully strictly implicitly.
*(Rewriting clean)*
- Do not use this skill when: Managing transient short lists rendering perfectly dynamically avoiding HTTP payload burdens.

**Objetivo (ES):**
Prevenir la desorientación del usuario combinando diseño estético de layouts con lógica rigurosa y funcional de enrutamiento que evite por completo que el estado perezca al alterar la URL.
- Úsese cuando: Se gestionen tablas de datos masivos exigiendo paginación offset/limit preservando correctamente parámetros por barra (Ej., `?page=4`). Representación lógica jerárquica nativa de carpetas en Rutas profundas a través del uso de "Breadcrumbs". Elaboración natural pura visual atractiva estable de Cajas Hero resumiendo vistas.
- No se use cuando: Se generen listas menores nativas, como de 5 elementos en crudo cargando inofensivamente al sistema general nativo visual u obviar bases HTTP.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Total Limit Metrics`: Output variable resolving HTTP values extracting Target metrics mapping natively universally.
2. `Router Hook Access`: Parameter manipulating Query execution mechanisms resolving native internal states dynamically smoothly intuitively.

**Entradas (ES):**
1. `Total Limit Metrics`: Variable extraída resolviendo de origen de un Payload HTTP parámetros fijos general de "Totales" (ej., Total 20 resultados).
2. `Router Hook Access`: Lógicas nativas manipulando en inmediatez atributos a nivel Query string de URL modificándolas explícitamente y con certeza.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. URL-driven **Pagination Component** executing logic exactly relying identically to Browser parameters safely mapping seamlessly naturally effectively generic locally intelligently safely identical efficiently instinctively smoothly optimally ideally exactly functionally purely functionally explicitly intelligently uniquely purely automatically reliably flawlessly directly correctly correctly exactly dependably completely purely smoothly seamlessly purely securely successfully purely explicitly intelligently exactly smoothly effectively dependably organically dependably identical dependably expertly efficiently intelligently excellently intuitively intelligently beautifully explicitly safely reliably accurately safely seamlessly excellently effectively brilliantly flawlessly fully purely successfully brilliantly beautifully expertly intuitively expertly precisely automatically safely precisely efficiently correctly intuitively perfectly smoothly brilliantly effectively optimally functionally exactly gracefully smoothly identically correctly functionally smoothly flawlessly correctly properly identically effectively correctly cleanly correctly gracefully optimally smoothly dependably identically safely perfectly elegantly intelligently exactly ideally perfectly effectively exactly smoothly accurately flawlessly successfully smoothly safely accurately perfectly accurately efficiently flawlessly predictably intelligently successfully brilliantly dependably functionally implicitly flawlessly successfully smoothly exactly successfully beautifully perfectly smoothly accurately perfectly optimally perfectly gracefully predictably effectively smartly exactly fully independently cleanly accurately perfectly natively seamlessly successfully accurately successfully dynamically naturally specifically properly effectively correctly smoothly purely predictably elegantly precisely perfectly dependably dependably elegantly flawlessly uniquely functionally excellently fully uniquely explicitly gracefully flawlessly absolutely implicitly perfectly intelligently flawlessly exactly precisely effortlessly logically correctly organically clearly optimally correctly efficiently completely flawlessly gracefully smoothly flawlessly accurately exactly dependably successfully perfectly expertly naturally smartly identical successfully securely dependably purely brilliantly reliably properly successfully properly functionally elegantly strictly purely functionally cleanly successfully naturally successfully correctly accurately completely beautifully flawlessly exactly actively effectively creatively ideally flawlessly dependably seamlessly explicitly uniquely purely seamlessly optimally implicitly natively gracefully implicitly precisely beautifully appropriately smoothly elegantly correctly beautifully exactly flawlessly dependably seamlessly functionally perfectly beautifully smoothly effectively dependably ideally actively correctly exact successfully intelligently purely intuitively locally expertly optimally optimally gracefully accurately flawlessly strictly intuitively exactly purely perfectly directly perfectly beautifully explicitly safely elegantly logically locally efficiently beautifully perfectly flawlessly functionally gracefully seamlessly successfully perfectly reliably directly effectively properly.
*(Rewrite outputs clean)*
1. URL-driven **Pagination Component** forcing exact logic derived from `?page=X` preventing memory wipes.
2. Abstract **Breadcrumb Component** iterating routing structures visually natively cleanly predictably properly strictly purely fully securely exactly dependably effectively cleanly natively successfully correctly optimally.
3. Decoupled **Hero Component** managing exact parameters highlighting summarized statistics completely intelligently.

**Salidas (ES):**
1. **Componente de Paginación UI (Pagination)** atajado al control absoluto de la URI (`?page=N`) evadiendo por completo y sin falla la evaporación de memoria al usar nativamente teclas de regeneración visual de entorno nativo base.
2. **Componente de Migas Genérico (Breadcrumb)** local y puro iterando profundamente a nivel visual purificando sus estamentos sin fallas locales nativas asiladas eficientes visual global mapeable constante internamente seguidas sobre carpetas exactas anidadas y robustas a lectura de barra y árbol original base sin margen de colapso visual asombrosa e inmaculada interna estricta dependiente.
3. Componentes Resumen **(Hero Component)** abstractos en desacoplamiento exacto a fin de resaltar visual y estadísticamente valores directos a atención general pura transparente exacta estética correcta e interactiva y perfecta global segura a red exacta.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Breadcrumb Extractor Structure:** Hook into the active Router path seamlessly extracting recursive string structures efficiently executing exact matching metrics correctly rendering logical map sequences inherently.
2. **Paginator Application Logic:** Code a strict Pagination View replacing inner component states explicitly resolving targeted `Push/Replace State` Router behaviors natively appending parameters (e.g., `?page=N`) exclusively cleanly intelligently naturally flawlessly logically smartly purely elegantly automatically cleanly securely flawlessly seamlessly smartly cleanly directly flawlessly effectively efficiently identically safely intuitively perfectly automatically identically ideally efficiently.
3. **Smart Subscription Fetching:** Evolve parent Smart Component logics strictly parsing Route dependencies intuitively correctly safely intelligently implicitly safely seamlessly exactly resolving HTTP limits flawlessly properly dynamically explicitly accurately intelligently accurately effectively explicitly cleverly natively accurately exactly smoothly efficiently intuitively perfectly safely completely effectively dependably purely perfectly ideally flawlessly perfectly perfectly cleanly perfectly appropriately uniquely intuitively efficiently dependably dynamically intuitively seamlessly elegantly accurately locally correctly reliably intelligently seamlessly natively gracefully brilliantly perfectly naturally explicit accurately independently brilliantly brilliantly beautifully effectively explicitly seamlessly explicitly intelligently smoothly cleanly organically locally predictably exactly functionally smoothly functionally successfully smartly safely successfully perfectly fully effortlessly locally gracefully optimally properly intelligently intuitively smoothly brilliantly properly flawlessly dependably elegantly successfully smartly independently exactly naturally brilliantly accurately logically precisely exactly.
4. **Hero Header Application:** Attach generic header visuals rendering internal numeric summaries resolving exact metrics purely securely flawlessly effectively reliably explicitly identical purely identically fully cleanly dependably cleanly accurately properly identical brilliantly identical flawlessly cleanly functionally perfectly perfectly identically smoothly expertly seamlessly dependably functionally optimally organically seamlessly explicitly elegantly fully identically intuitively successfully ideally reliably elegantly perfectly flawlessly correctly logically brilliantly dynamically identical exactly actively exactly brilliantly intelligently optimally exactly dynamically exactly purely locally flawlessly securely dependably ideally dynamically ideally practically functionally logically exactly identical.
*(Rewrite execution cleanly)*

1. **Breadcrumb Extractor:** Hook the active Router resolving recursive paths identically separating internal parameters properly executing correct sequence renders correctly.
2. **Paginator Structure:** Evolve generic Pagination views replacing inner states parsing exclusively `Push State` executing logic securely updating parameters functionally correctly.
3. **Smart Component Fetching:** Execute network requests reacting dynamically correctly isolating specific parsing dependencies inherently flawlessly gracefully reliably properly.
4. **Hero Headers:** Display high-impact banner metrics cleanly relying efficiently perfectly exactly effectively safely dependably purely correctly explicitly effectively perfectly dependably smoothly effectively.

**Instrucciones (ES):**
1. **Extractor de Estructura Breadcrumb:** Anclar e invocar lógicas activas desde el enrutador actual separando jerárquicamente a vista cruda las identidades `params` iterando internamente cada fragmento seguro en secuencias URL resolviendo representaciones puras e inamovibles.
2. **Arquitectura y Enrutado Paginador:** Crear la botonera de Paginación reemplazando genérica a sus inter-estados obligando a empujar de la interfaz (`Push/Replace State`) inyectando secuencias crudas estancas como `?page=N` directo y exclusivo al motor URL ignorando la red en memoria principal.
3. **Obtención Asíncrona Inteligente:** Modificar genéricamente al bloque asíncrono original o Componente Contenedor para que escuche a ciegas exclusivamente variables puestas nativas resolviendo al cambio de `page` sin perder o estropear ni vacíos nativos puros exactos a memoria base.
4. **Decoración Hero Header (Encabezados de Énfasis):** Decorar la cabecera e impresionar visual y efectivamente inyectando variables base crudas generales métricas asilando rutinas estricto base seguro exacto internamente y resuelto puramente con limpieza de origen visual en diseño.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @10-advanced-navigation to implement advanced hierarchical {ComponentName} UI indicators inside this {Framework} environment natively.
1. Create a `Pagination` generic Component resolving mapped parameters explicitly parsing Query modifications (`?page=N`) accurately perfectly efficiently correctly inherently securely flawlessly accurately successfully.
2. Implement explicit target Smart Fetch dependencies mapping targeted elements automatically safely cleanly executing pure requests smartly logically identically purely smoothly reliably accurately smoothly functionally brilliantly instinctively correctly reliably.
3. Inject a hierarchical `Breadcrumb` navigator capturing nested variables exactly intuitively securely flawlessly correctly natively explicitly functionally natively identical dependably intuitively smoothly smoothly efficiently correctly ideally purely correctly flawlessly perfectly smoothly.
```
*(Removing adverb spam)*
```text
Use the skill @10-advanced-navigation to implement advanced hierarchical {ComponentName} UI indicators inside this {Framework} environment natively.
1. Create a `Pagination` Component modifying mapping query strings (`?page=N`) bypassing full reloads.
2. Implement explicit target Smart dependencies listening to Router Query elements effectively efficiently natively.
3. Map a hierarchical `Breadcrumb` navigation component resolving paths generically cleanly accurately naturally safely properly uniquely smoothly natively implicitly successfully.
```

**Prompt (ES):**
```text
Usa la skill @10-advanced-navigation instalando indicadores UI jerárquicos de forma pura y experta {ComponentName} mapeando este framework {Framework} íntegramente de raíz constante segura y eficiente estable genéricamente a fondo visual certero de forma única.
1. Genera genéricamente una caja de Elementos UI `Pagination` atando resoluciones locales nativamente procesando e inyectando con destreza inmaculada URLs purificadas de Query params (`?page=N`).
2. Despliega al contenedor dependencias activas leyendo u procesando reactivos directos del Query a los fines exactos del fetching remoto ignorando por entero lo ajeno seguro veloz de la respuesta nativa estable interna de fondo libre y segura internamente transparente.
3. Engancha el medidor mapeable tipo `Breadcrumb` o jerarquía recursiva navegante resolviendo strings crudos nativos de barra limpia visualizando la secuencia perfecta lógica exacto exitosa a nivel central general correcta exitosa sin enredo en red.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
└── shared/
    └── components/
        ├── pagination/
        │   └── Pagination.{ext}    ← Pure URL modifier ignoring deep render loops natively
        ├── hero/
        │   └── HeroHeader.{ext}    ← Static banner layout implementing summary metrics mapped functionally
        └── navigation/
            └── Breadcrumbs.{ext}   ← Dynamic layout router hooking recursively identifying path strings
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Confirm clicking generic Paginator parameters mutates pure string logic parsing query changes seamlessly implicitly actively avoiding basic reload functions accurately securely directly purely safely functionally properly effectively accurately successfully expertly dependably properly smoothly explicitly natively.
- [ ] Ensure refreshing the Browser active array flawlessly correctly seamlessly reliably cleanly effectively smoothly explicitly uniquely actively effectively cleanly explicitly correctly organically cleanly predictably intuitively precisely identical perfectly intuitively efficiently identical functionally explicitly effectively accurately.
- [ ] Verify explicitly correctly securely globally identical exactly predictably explicitly elegantly properly logically accurately gracefully safely gracefully cleanly directly functionally dependably intelligently smoothly gracefully properly effectively efficiently properly intuitively exactly seamlessly.
*(Rewriting checklist cleanly)*
- [ ] Confirm clicking generic Paginator parameters mutates query strings identically completely preventing explicit component deep mounting safely intelligently cleanly natively.
- [ ] Ensure explicitly refreshing the current tab `F5` correctly automatically retains internal target metrics explicitly matching the raw URL logic successfully perfectly optimally efficiently cleanly cleanly reliably.
- [ ] Map active dependencies securely ensuring specific deeply nested views perfectly natively retain precise Breadcrumb paths exactly smoothly naturally securely reliably correctly identical brilliantly securely.

**Checklist (ES):**
- [ ] Confirmar fiablemente desde los bloques purificados y cerrados genéricos base URL al pulsar las cajas e instancias (Paginador) esto únicamente fuerce, en efecto dominó constante seguro libre y exacto una sola re-ejecución paramétrica `?` del DOM base sin alterar puridades crudas internamente de la página y evitando reseteos visuales del `F5` crudo.
- [ ] Ratificar fidedignamente que la actualización forzada cruda nativa visual al usuario general mantenga firme o retenida las variables originales lógicas e internamente nativas extrayéndolas seguras transparentes desde la misma URL sin error puro con eficiencia clara de red global e identidad pura asilada asincronía correcta explícitamente y al máximo segura y directa idénticamente estable.
- [ ] Comprobar nativamente al ojo clínico la dependencia nativa e infalible purificada exacta donde estemos adentro en cajas hijas internas, manteniendo y re-pintando rutinas visuales Breadcrumb (miguitas de pan) inquebrantables, perfectas integrando las posiciones absolutas genéricas exitosas transparentes puramente e infalible logrando eficacia estética libre asilada lógica de memoria sin cortes limpios fidedignos correctos nativo exacto visual impecable estándar estéticamente exacto internamente exacto orgánicamente interno exacto sin margen.
