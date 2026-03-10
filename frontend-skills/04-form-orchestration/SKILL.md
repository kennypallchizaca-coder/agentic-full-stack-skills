---
name: 04-form-orchestration
description: "Establishes systematic data collection implementing Reactive/Controlled Forms. Provides robust client-side validation logic avoiding primitive boilerplate and managing internal form states (Pristine, Dirty, Invalid, Submitting)."
risk: medium
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Forms represent the principal gateway for data ingestion. Manually attaching `onKeyUp` listeners to 20 inputs results in disastrous performance rendering bottlenecks and unmaintainable state shapes. This skill implements programmatic form orchestration ensuring validation engines (e.g., Zod, Yup) interact safely with data states before any API submit.

**Descripción (ES):**
Los formularios representan la principal puerta de entrada para la ingesta de datos. Adjuntar detectores `onKeyUp` manualmente a 20 inputs resulta en cuellos de botella desastrosos en el rendimiento de renderizado y formas de estado imposibles de mantener. Esta skill implementa una orquestación programática del formulario asegurando que los motores de validación (ej., Zod, Yup) interactúen de forma segura con los estados de los datos antes de ejecutar cualquier submit a la API.

---

# 2. Skill Objective

**Objective (EN):**
Implement a standardized form control system preventing faulty or malicious payloads from being triggered against HTTP clients.
- Use this skill when: Standardizing Login, Configuration Settings, and intricate Dashboard entity creation.
- Do not use this skill when: Implementing a single, simplistic "Search Box" filtering an existing array.

**Objetivo (ES):**
Implementar un sistema de control de formulario estandarizado previniendo que payloads defectuosos o maliciosos se envíen a los clientes HTTP.
- Úsese cuando: Se estandarice un Inicio de sesión (Login), Configuraciones y creación intrincada de entidades en el Dashboard.
- No se use cuando: Se implemente una simple y única "Caja de Búsqueda" para filtrar un arreglo existente.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Form Manager`: `React Hook Form`, `VueForm`, `@angular/forms` (Reactive).
2. `Validation Schema`: `Zod`, `Yup` Native Validators natively defined.

**Entradas (ES):**
1. `Form Manager`: `React Hook Form`, `VueForm`, `@angular/forms` (Reactive).
2. `Validation Schema`: `Zod`, `Yup` o Validadores Funcionales nativos.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Implementation of Controlled or Reactive Form Instances cleanly mapped natively.
2. Presentation layers managing HTML error rendering gracefully parsing target matrix rules universally.

**Salidas (ES):**
1. Implementación limpia y nativamente estructurada de Instancias de Formulario Controladas o Reactivas.
2. Capas de presentación gestionando el error HTML elegante y nativamente mediante parseo de la matriz de validaciones globales.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Schema Initialization:** Define the internal Type object matching target HTTP Data Transfers parsing strict field limits (`Zod`).
2. **Form Manager Subscription:** Invoke programmatic libraries injecting identical validation mechanisms assigning Initial State parameters generically to bypass layout rendering artifacts entirely.
3. **Template Data Binding:** Tie explicitly targeted Input attributes effectively eliminating unique arbitrary elements replacing ID dependencies globally with exact hook/provider methods generically (`register('name')` or `formControlName="name"`).
4. **Submit Lock Mechanisms:** Execute Native HTML binding forcing Button attributes declaring specific `disabled` statuses querying internal `.isSubmitting` tracking safely preventing network API duplications effortlessly.

**Instrucciones (ES):**
1. **Inicialización del Esquema:** Definir el Tipo del objeto interno compatible con Data Transfers de HTTP que se deben apuntar procesando las reglas de los límites nativos (Ej, uso de `Zod`).
2. **Suscripción de las librerías al Gestor del Form (Form Manager):** Invocación y ejecución genérica que inyecta los mecanismos de validadores de forma paralela asignando estados predeterminados iniciales evitando daños colaterales a otros renderizados visuales asíncronos en pantalla.
3. **Data Binding (Modelo Lógico-Vista):** Atar explícitamente y nativamente atributos hacia los Inputs eficientemente deshaciéndose de etiquetas únicas o ancladas por `ID` suplantando los mismos nativamente hacia Providers exactos o hooks genéricamente compatibles (como un `register('nombre')` o `formControlName="nombre"`).
4. **Tácticas/Mecanismos de Cierre Submit Lock:** Aplicar HTML natural imponiendo candados a la directiva de sus parámetros `disabled` extrayendo el estatus nativo de verificación `isSubmitting` desde sus adentros rastreándolo e impidiendo así cualquier inyección accidental a nivel API en forma repetitiva o dobleces inútiles.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @04-form-orchestration to programmatically control a standard {UseCase} form structure in this {Framework} environment using {FormManagerLibrary}.
1. Enforce strict type validation definitions leveraging {ValidationSchemaLibrary} capturing necessary error messages.
2. Bind the inputs logically to track `Pristine`, `Dirty`, and `Invalid` DOM behaviors.
3. Design the Submit execution explicitly mapping payload properties avoiding raw DOM iterations or querySelectors.
```

**Prompt (ES):**
```text
Usa la skill @04-form-orchestration para controlar programáticamente una estructura estándar {UseCase} en un ambiente {Framework} a base del uso de un {FormManagerLibrary}.
1. Forzar una definición e validación exacta usando este mecanismo {ValidationSchemaLibrary} a través de la captación interna y el registro oportuno nativo.
2. Enlazar de manera lógica atributos a fin de rastrear conductas HTML basadas en dominios Pristine/Dirty/Invalid dentro del DOM local visiblemente expuesto.
3. Redactar el proceso ejecutable al ocurrir un Submit extrayendo nativamente estos mismos properties mapeados sin involucrar NINGUNA clase de consulta externa, como un simple e ingenuo `querySelector`.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
└── features/
    └── {EntityName}/
        └── components/
            ├── {EntityName}Form.{ext}          ← Controlled/Reactive Form Presentation
            └── {EntityName}Form.schema.{ts}    ← Decoupled Validation Matrix (e.g., zod schema)
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Confirm no native `document.getElementById('input').value` generic parsing rules are mapped randomly inside standard scopes.
- [ ] Certify Buttons block user interaction natively disabling network functionality intelligently analyzing ongoing submission queries dynamically.
- [ ] Guarantee error messages accurately display gracefully strictly once the target cursor `blur` property successfully finishes tracking `touched` logic natively.

**Checklist (ES):**
- [ ] Validar por seguro de forma paralela nativamente que NINGÚN parseo primitivo u objetos como este `document.getElementById('input').value` ande metido nativamente rondando cerca o por un Scope común de cualquier módulo existente de ningún proyecto frontend visual al ser enviado.
- [ ] Homologar y asegurar por cuenta local u oficial paralela genéricamente bloqueos internos (deshabilitar o disable del Button en modo HTML simple) operativamente hasta dar su propio fallo a fin de impedir enviar peticiones duplicadas a los backends.
- [ ] Prometer legalidad, asegurar visualización, advertencias y renderizados exactos visualizados una vez detectadas pérdidas estandarizadas lógicas directas provocando blurs sin interrupciones sobre áreas vacías `touched` de forma pura.
