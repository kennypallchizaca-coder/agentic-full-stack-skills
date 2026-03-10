---
name: 01-project-setup
description: "Establishes the foundational configuration for a Single Page Application (SPA) or Static Site Generator (SSG). Enforces strict TypeScript typing, absolute path aliasing (@/), and secure environment variable management."
risk: low
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
A robust frontend starts with absolute predictability. Relying on endless relative paths (`../../../components`) creates brittle refactoring scenarios, while exposing internal backend API keys accidentally to the client results in fatal security flaws. This skill standardizes the architectural foundation configuring precise compiler behaviors before writing visual code.

**Descripción (ES):**
Un frontend robusto comienza con una previsibilidad absoluta. Depender de rutas relativas infinitas (`../../../components`) crea escenarios de refactorización frágiles, mientras que exponer accidentalmente claves de API internas del backend al cliente resulta en fallos de seguridad fatales. Esta skill estandariza la base arquitectónica configurando comportamientos precisos del compilador antes de escribir código visual.

---

# 2. Skill Objective

**Objective (EN):**
Initialize the frontend core structure enforcing robust TypeScript boundaries, clean import aliases, and public-facing environment abstractions.
- Use this skill when: Initializing a brand-new repository or resolving chaotic import path structures (Refactoring "Module Not Found" cascades).
- Do not use this skill when: Modifying an external library node_modules dependency explicitly.

**Objetivo (ES):**
Inicializar la estructura central del frontend aplicando límites robustos de TypeScript, alias de importación limpios y abstracciones de entorno orientadas al entorno público.
- Úsese cuando: Se inicializa un repositorio nuevo o se resuelven estructuras caóticas de rutas de importación (Refactorización de cascadas "Module Not Found").
- No se use cuando: Se modifica dependencias explícitas externas de node_modules.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Frontend Framework`: React, Angular, Vue, or Astro.
2. `Bundler`: Webpack, Vite, or CLI Native.
3. `Env Variables`: The keys that require client exposure.

**Entradas (ES):**
1. `Frontend Framework`: React, Angular, Vue o Astro.
2. `Bundler`: Webpack, Vite o CLI Nativo.
3. `Env Variables`: Las claves que requieren exposición al cliente.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Standardized `tsconfig.json` configurations.
2. `vite.config.ts` or `angular.json` route mappers.
3. `.env` and `.env.example` templates enforcing public prefixes (e.g., `VITE_API_URL`).

**Salidas (ES):**
1. Configuraciones estandarizadas en `tsconfig.json`.
2. Mapeadores de rutas en `vite.config.ts` o `angular.json`.
3. Plantillas `.env` y `.env.example` imponiendo prefijos públicos (ej. `VITE_API_URL`).

---

# 5. Execution Steps

**Instructions (EN):**
1. **TypeScript Auditing:** Target `tsconfig.json`. Enforce `"strict": true`, `"noImplicitAny": true`, and ensure `"paths"` is instantiated.
2. **Setup Absolute Aliasing:** Define the `@/*` alias pointing universally to the `src/*` directory ensuring top-level path resolution ignores relative nesting entirely.
3. **Bundler Synchronization:** Replicate the alias logic exclusively inside the framework Bundler (e.g. `resolve.alias` in Vite).
4. **Environment Bootstrapping:** Create a `.env` root file containing the `API_URL`. Ensure the variable prefix perfectly matches the strict Framework requirement (e.g. `VITE_` or `PUBLIC_`) to guarantee it becomes readable within the client Javascript `window` boundary securely.

**Instrucciones (ES):**
1. **Auditoría de TypeScript:** Apunta a `tsconfig.json`. Aplica `"strict": true`, `"noImplicitAny": true` y asegúrate de instanciar `"paths"`.
2. **Configurar Alias Absoluto:** Define el alias `@/*` apuntando universalmente al directorio `src/*` asegurando que la resolución de rutas de nivel superior ignore por completo anidamientos relativos.
3. **Sincronización del Bundler:** Replica la lógica del alias exclusivamente dentro del Bundler del framework (ej. `resolve.alias` en Vite).
4. **Inicialización de Entorno:** Crea un archivo raíz `.env` que contenga la `API_URL`. Asegúrate de que el prefijo de la variable coincida perfectamente con el requisito estricto del Framework (ej. `VITE_` o `PUBLIC_`) para garantizar que se vuelva legible de forma segura dentro del límite Javascript del cliente.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @01-project-setup to map foundational properties in this {Framework} codebase.
1. Configure `tsconfig` and the underlying {Bundler} assigning the `@/` absolute alias focusing universally on `src/`.
2. Generate base `.env` structures exposing the strict Variable Prefix required by the framework pointing explicitly to `{API_URL}`.
```

**Prompt (ES):**
```text
Usa la skill @01-project-setup para mapear las propiedades fundamentales en este código base de {Framework}.
1. Configura `tsconfig` y el {Bundler} subyacente asignando el alias absoluto `@/` enfocándose universalmente en `src/`.
2. Genera estructuras base `.env` exponiendo el prefijo de variable estricto requerido por el framework apuntando explícitamente a `{API_URL}`.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
/
├── .env.development        ← Local API mapping (Never commit)
├── .env.example            ← Template structure (Commit safely)
├── tsconfig.json           ← Compiler path bindings
└── vite.config.{ts}        ← Bundler synchronized execution
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Attempting an import like `import {x} from '@/core'` correctly resolves without Node terminal pathing crashes.
- [ ] Creating an unused `any` type forces the IDE TS-Server to instantly visualize a red underlining error boundary.
- [ ] Using `import.meta.env` or `process.env` successfully prints the targeted `.env` string natively to the Browser Console.

**Checklist (ES):**
- [ ] Intentar un import como `import {x} from '@/core'` se resuelve correctamente sin caídas de rutas en la terminal de Node.
- [ ] Crear un tipo `any` sin usar obliga al Servidor TS del IDE a visualizar instantáneamente un límite de error subrayado en rojo.
- [ ] Usar `import.meta.env` o `process.env` imprime exitosamente el string nativo apuntado desde `.env` a la Consola del Navegador.
