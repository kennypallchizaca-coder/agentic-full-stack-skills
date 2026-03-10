---
name: 05-ui-feedback-system
description: "Establishes global communication interfaces for the UI layer preventing silent systemic failures. Standardizes Global Toast Notifications and Confirmation Action Modals ensuring consistent visual feedback."
risk: low
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
A user executing an action (e.g., "Add Record") and experiencing nothing—no loading spinner, no success message, no error alert—represents severe UX degradation. This skill implements a universal notification system designed so that HTTP Interceptors or nested Child Components can trigger visual alerts centrally without redefining popup logic on every single page.

**Descripción (ES):**
Un usuario que ejecuta una acción (ej., "Agregar Registro") y no experimenta nada —ni spinner de carga, ni mensaje de éxito, ni alerta de error— representa una degradación severa de la Experiencia de Usuario (UX). Esta skill implementa un sistema de notificación universal diseñado para que los Interceptores HTTP o componentes hijos anidados puedan activar alertas visuales de forma centralizada sin redefinir la lógica de los popups en absolutamente todas las páginas.

---

# 2. Skill Objective

**Objective (EN):**
Implement standardized UI signals decoupled from specific component business logic.
- **Toasts:** Non-blocking, temporary slide-in messages for Success/Error notifications.
- **Confirmation Modals:** Blocking UI dialogs enforcing strict user acknowledgment prior to destructive operations (e.g., deleting user profiles).
- Use this skill when: An action operates asynchronously through the backend and requires final status visibility.
- Do not use this skill when: Alerting local, trivial validation errors (e.g., "Your password is too short"); those belong attached to the inputs inherently mapped in Skill 04.

**Objetivo (ES):**
Implementar señales UI estandarizadas desacopladas de la lógica de negocio específica del componente.
- **Toasts:** Mensajes temporales deslizables no bloqueantes para notificaciones de Éxito/Error.
- **Confirmation Modals:** Diálogos UI bloqueantes forzando estricto reconocimiento del usuario previo a operaciones destructivas (ej., borrar perfiles de usuario).
- Úsese cuando: Una acción opera asíncronamente a través del backend y requiere visibilidad final de su estado.
- No se use cuando: Se alerten errores de validación triviales locales (ej., "Tu contraseña es muy corta"); esos pertenecen adheridos a los inputs mapeados inherentemente en la Skill 04.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `UI Library`: Utility Framework (e.g., Tailwind, DaisyUI) or native custom CSS (Skill 07).
2. `Trigger Method`: Exposed Global Service or State Function to spawn notifications.

**Entradas (ES):**
1. `UI Library`: Framework de Utilidades (ej., Tailwind, DaisyUI) o CSS personalizado nativo (Skill 07).
2. `Trigger Method`: Servicio Global Expuesto o Función de Estado para generar notificaciones.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Global `ToastContainer` persisting exclusively in the Main Layout root natively.
2. Abstract Services or Event Maps broadcasting strings globally (`NotificationService.showError("Failed to update.")`).
3. Reusable Dialog Dumb Component supporting standardized callback parameter configurations (`onConfirm={...}`).

**Salidas (ES):**
1. Un `ToastContainer` global persistiendo exclusivamente en la raíz del Main Layout nativamente.
2. Servicios Abstractos o Mapas de Eventos transmitiendo strings globalmente (`NotificationService.showError("Error al actualizar.")`).
3. Componente genérico Dumb Reutilizable de tipo Dialog respaldando configuraciones de parámetros callback estandarizados (`onConfirm={...}`).

---

# 5. Execution Steps

**Instructions (EN):**
1. **Implement Toast State Manager:** Define a central array structure storing transient notification objects (`{id, message, type: success|error|warn, timeout}`). Store this in a generic Global provider or Service natively avoiding component entanglement.
2. **Setup Root Layout Rendering:** Generate a standard `<ToastContainer />` located at the highest app node (or utilizing `Portals/teleport`). It subscribes to the variable changes rendering absolute positioned `<Toast />` nodes systematically.
3. **Establish Service Broadcaster:** Export simple generic helper interfaces (e.g., `toast.error(message)` ). When invoked, natively append the message to the store memory, setup an automatic 3000ms removal delay hook cleaning the targeted object implicitly from the active UI without manual involvement natively.
4. **Integrate Dialog Modals:** Generically generate robust fullscreen backdrops applying strictly pure CSS constraints (`z-index`) controlling DOM parameters manually exposing purely generic callbacks parsing Promise outputs naturally.

**Instrucciones (ES):**
1. **Implementar el Gestor de Estado para Toasts:** Define una estructura central tipo array (arreglo) almacenando objetos transitorios de notificaciones (`{id, message, type: success|error|warn, timeout}`). Almacénalo en un proveedor o Servicio Global genérico nativamente evitando enredos con el componente.
2. **Setup del Renderizado Raíz (Root Layout):** Genera un `<ToastContainer />` estándar localizado en el nodo más alto de la app (o utilizando `Portals/teleport`). Este se suscribe a los cambios de la variable renderizando los nodos `<Toast />` en posición absoluta sistemáticamente.
3. **Establecer el Transmisor (Broadcaster) del Servicio:** Exporta interfaces auxiliares genéricas y simples (ej., `toast.error(message)`). Cuando se invoque, añade el mensaje nativamente a la memoria del store, configura un retraso automático (`delay`) de limpieza de 3000ms eliminando el objetivo de la UI activa implícitamente sin intervención manual de origen nativo.
4. **Integrar Modales de Diálogo:** Generar genérica y robustamente fondos oscuros o traslúcidos a pantalla completa aplicando estrictamente restricciones CSS puras (`z-index`) controlando parámetros DOM y exponiendo puramente callbacks genéricos interpretando salidas en Promise (Promesas) naturalmente.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @05-ui-feedback-system to build a programmatic UI Feedback system inside this {Framework} project structure.
1. Implement a Global Toast store holding internal mapping Array elements cleanly.
2. Render the `ToastContainer` absolutely using {CSSFramework} constraints (e.g., DaisyUI `toast` variables or raw CSS metrics).
3. Export an accessible functional Service extracting `{showSuccess, showError}` mechanisms safely managing a rigid automatic 3-second DOM elimination loop locally.
```

**Prompt (ES):**
```text
Usa la skill @05-ui-feedback-system para programar e implementar de manera generalizada y limpia rutinas y sistemas UI dentro de este {Framework} directamente.
1. Implementa una variable en la lógica de memoria guardando un Array y el mapeo de elementos limpios que persistan.
2. Renderiza el envoltorio `ToastContainer` de manera totalmente externa aplicando constraints del mismo entorno visual subyacente de {CSSFramework} (ej. Uso de marcadores DaisyUI, vars Tailwind y dimensiones en crudo).
3. Exporta con seguridad Servicios en el framework que extraigan una vez `{showSuccess, showError}` proveyendo bucles estrictos que eliminen de facto su presencia a lo largo de un timing auto-convenido DOM de tan solo 3 segundos en paralelo.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
└── shared/
    ├── components/
    │   ├── feedback/
    │   │   ├── ToastContainer.{ext}   ← Loop renderer injected into Root Array
    │   │   ├── Toast.{ext}            ← Custom Visual Design
    │   │   └── ConfirmModal.{ext}     ← Dumb backdrop executing passed Closures
    └── ui/
        └── Notification.service.{ts}  ← Logical array manipulation methods
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Confirm Toast overlays stack correctly atop other interactive elements (`z-index` properties) across all routing viewports generically.
- [ ] Ensure that Backend generic API responses automatically bounce their 500 error outputs reliably directly rendering target overlay models actively executing without un-needed extra logic natively.
- [ ] Avoid primitive memory leaks natively confirming raw timeouts accurately terminate without active variables remaining isolated un-targeted accurately.

**Checklist (ES):**
- [ ] Ratificar superposiciones confirmadas montadas sobre topes y etiquetas absolutas nativas correctas interactuando por su variable z-index frente a diversas páginas (rutas).
- [ ] Asegurarse que errores Backend puros 500 se proyecten automática, transparente y eficientemente desplegando salidas por overlays programadas al origen nativo en general y local de manera limpia.
- [ ] Impedir derramamientos o perdidas de memoria al revisar puntitos remotos `timeouts` limpiando cualquier var residual o bloque no asignado con una asertividad correcta pura.
