---
name: 05-ui-feedback-system
description: "Standardizes feedback, loading communication, confirmation flows, and heuristic review criteria so UI behavior stays usable across frameworks."
risk: low
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Users need clear feedback when something is loading, succeeds, fails, or requires confirmation. This skill centralizes those signals and the heuristic review criteria that keep messages, dialogs, loading states, and recovery flows understandable across applications.

**Descripción (ES):**
Los usuarios necesitan feedback claro cuando algo está cargando, sale bien, falla o requiere confirmación. Esta skill centraliza esas señales y los criterios heurísticos que mantienen comprensibles los mensajes, dialogos, estados de carga y flujos de recuperación en distintas aplicaciónes.

Related resources:
- [usability-accessibility-checklist.md](./resources/usability-accessibility-checklist.md)
- [ux-heuristics-reference.md](./resources/ux-heuristics-reference.md)

---

# 2. Skill Objective

**Objective (EN):**
Build a shared feedback layer for transient notifications, confirmations, loading communication, and heuristic-quality review that fits the target UI architecture.
- Use this skill when: The app performs async operations that need visible success, error, warning, confirmation, or recovery guidance.
- Do not use this skill when: The issue is a field-level válidation error that belongs inside the form itself.

**Objetivo (ES):**
Construir una capa compartida de feedback para notificaciones transitorias, confirmaciónes, comúnicación de carga y revision heuristica de calidad que encaje con la arquitectura UI objetivo.
- Úsese cuando: La app ejecute operaciónes asíncronas que necesiten feedback visible de éxito, error, advertencia, confirmación o recuperación.
- No se use cuando: El problema sea un error de válidación por campo que deba vivir dentro del formulario.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Feedback Channel`: Toast system, alert system, modal/dialog layer, inline message pattern, or global loading indicator.
2. `Trigger Source`: Components, repositories, interceptors, or shared services.
3. `Visual Strategy`: Framework UI library, custom CSS system, or design-system components.
4. `Usability Constraints`: Focus management, keyboard escape, contrast, ARIA labels, copy clarity, and error-prevention expectations.

**Entradas (ES):**
1. `Feedback Channel`: Sistema de toasts, alertas, modales, patrón de mensajes inline o indicador global de carga.
2. `Trigger Source`: Componentes, repositorios, interceptores o servicios compartidos.
3. `Visual Strategy`: Libreria UI del framework, sistema CSS propio o componentes del design system.
4. `Usability Constraints`: Gestion de foco, escape por teclado, contraste, etiquetas ARIA, claridad del copy y expectativas de prevención de errores.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. A global feedback container mounted near the app shell.
2. Simple service or store APIs to trigger feedback.
3. Reusable confirmation, loading, and recovery patterns.
4. A heuristic review baseline for message clarity, user control, consistency, and accessibility.

**Salidas (ES):**
1. Un contenedor global de feedback montado cerca del shell de la app.
2. APIs simples via servicio o store para disparar feedback.
3. Patrones reutilizables de confirmación, carga y recuperación.
4. Una base heuristica de revision para claridad del mensaje, control del usuario, consistencia y accesibilidad.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Create one shared feedback entry point:** Mount toast and dialog containers near the top-level app layout.
2. **Differentiate channel types:** Inline válidation belongs near the field; toasts are transient; destructive actions require explicit confirmation; empty and loading states belong in the page or section that owns the wait.
3. **Expose simple trigger APIs:** Use calls such as `notify.success`, `notify.error`, `confirm.open`, or `loading.start`.
4. **Preserve focus and keyboard flow:** Confirmation dialogs should trap focus when open, return focus when closed, and support keyboard dismissal where appropriate.
5. **Write recovery-friendly messages:** Prefer actionable copy, explicit destructive labels, and messages that tell users what they can do next.
6. **Review with heuristics, not only visuals:** Check visibility of system status, match with user language, user control, error prevention, recognition over recall, consistency, and accessible interaction patterns.
7. **Clean up automatically:** Toast timeouts and dialog lifecycle should not leak listeners or stale state.
8. **Adapt the pattern, not the literal example:** Rename files, channels, helpers, and UI primitives to match the target project's framework, design system, and business language.

**Instrucciones (ES):**
1. **Crea un punto compartido de feedback:** Monta contenedores de toast y dialogo cerca del layout principal de la app.
2. **Diferencia tipos de canal:** La válidación inline vive junto al campo; los toasts son transitorios; las acciones destructivas requieren confirmación explícita; los estados vacios y de carga viven en la página o seccion que posee la espera.
3. **Expone APIs simples para dispararlos:** Usa llamadas como `notify.success`, `notify.error`, `confirm.open` o `loading.start`.
4. **Preserva foco y flujo de teclado:** Los dialogos de confirmación deben atrapar el foco al abrirse, devolverlo al cerrarse y soportar dismissal por teclado cuando corresponda.
5. **Escribe mensajes que ayuden a recuperarse:** Prefiere copy accionable, etiquetas destructivas explícitas y mensajes que indiquen que puede hacer después el usuario.
6. **Revisa con heuristicas, no solo con visuales:** Verifica visibilidad del estado del sistema, lenguaje cercano al usuario, control del usuario, prevención de errores, reconocimiento sobre recuerdo, consistencia y patrónes accesibles.
7. **Limpia automaticamente:** Los timeouts de toast y el ciclo de vida de dialogos no deben dejar listeners o estado obsoleto.
8. **Adapta el patrón, no el ejemplo literal:** Renombra archivos, canales, helpers y primitivas UI para ajustarlos al framework, design system y lenguaje de negocio del proyecto objetivo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @05-ui-feedback-system to standardize feedback in this {Framework} app.
1. Add a shared toast, confirmation, and loading layer near the main app shell.
2. Expose simple helper APIs so features can show success, error, warning, and recovery guidance consistently.
3. Review the result against usability and accessibility heuristics, not only visual consistency.
```

**Prompt (ES):**
```text
Usa la skill @05-ui-feedback-system para estándarizar el feedback en esta app {Framework}.
1. Agrega una capa compartida de toasts, confirmaciónes y carga cerca del shell principal.
2. Expon helpers simples para que los features muestren éxito, error, advertencia y recuperación de forma consistente.
3. Revisa el resultado contra heuristicas de usabilidad y accesibilidad, no solo contra consistencia visual.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
└── shared/
    ├── components/
    │   └── feedback/
    │       ├── ToastContainer.{ext}
    │       ├── ConfirmDialog.{ext}
    │       ├── LoadingState.{ext}
    │       └── EmptyState.{ext}
    ├── services/ or stores/
    │   └── notification.{ext}
    └── ux/
        └── heuristics.{ext}
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Async success and error states surface through a shared feedback system.
- [ ] Destructive actions require explicit confirmation.
- [ ] Loading, empty, and recovery states are visible where the user needs them.
- [ ] Dialogs and feedback preserve focus, keyboard flow, and clear labeling.
- [ ] Message copy helps the user recover instead of only reporting failure.
- [ ] Names, files, channels, helpers, and UI primitives were adapted to the target project instead of copying the example structure literally.

**Checklist (ES):**
- [ ] Los estados asíncronos de éxito y error se muestran mediante un sistema compartido de feedback.
- [ ] Las acciones destructivas requieren confirmación explícita.
- [ ] Los estados de carga, vacio y recuperación son visibles donde el usuario los necesita.
- [ ] Los dialogos y el feedback preservan foco, flujo de teclado y etiquetado claro.
- [ ] El copy ayuda al usuario a recuperarse en lugar de solo reportar el fallo.
- [ ] Los nombres, archivos, canales, helpers y primitivas UI se adaptaron al proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
