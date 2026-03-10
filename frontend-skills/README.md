# 🎨 Universal Frontend Skills
### The Ultimate Collection of 12 Agentic Skills for React, Angular, Vue, and Astro
**React · Angular · Vue · Astro · TypeScript · Vite · Webpack**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-10-blueviolet)]()
[![Cursor](https://img.shields.io/badge/Cursor-✓-black)]()
[![Claude Code](https://img.shields.io/badge/Claude_Code-✓-orange)]()

---

## 🚀 Welcome to Frontend Skills

Just like the Backend universal skills library, this repository provides **12 Universal Agentic Skills** for frontend applications. They teach your AI Assistant how to implement robust architectures, global states, protected routing, and professional API consumption without making spaghetti code.

Regardless of whether you use **React**, **Angular**, **Vue** or **Astro**, the architectural flow is identical.

### How to use

Copy this `frontend-skills/` directory into your project root (or inside `.cursor/skills` / `.claude/skills`).

Then tell your AI:
> "Use the **@06-data-fetching** skill to configure Axios and the JWT Request Interceptor."

> "Follow **@02-component-architecture** to separate my `InvoiceView` from my `InvoiceForm` component."

---

## 📚 Browse the 12 Frontend Skills

| # | Skill | Descripción | Risk |
|---|-------|-------------|:----:|
| 01 | [**01-project-setup**](./01-project-setup/SKILL.md) | Setup inicial: aliases `@/`, linter, TS strict y archivos `.env` | 🟢 Low |
| 02 | [**02-component-architecture**](./02-component-architecture/SKILL.md) | Separación obligatoria de Smart Component vs Dumb Component | 🟢 Low |
| 03 | [**03-routing-strategy**](./03-routing-strategy/SKILL.md) | Enrutador global con Layouts y soporte de Lazy Loading | 🟡 Med |
| 04 | [**04-form-orchestration**](./04-form-orchestration/SKILL.md) | Formularios controlados sin petición, validación visual y DTOs | 🟡 Med |
| 05 | [**05-ui-feedback-system**](./05-ui-feedback-system/SKILL.md) | Estandarización de modales de alerta y Toast notifications globales | 🟢 Low |
| 06 | [**06-authentication-flow**](./06-authentication-flow/SKILL.md) | Flujo JWT (Respuesta HTTP -> Storage -> Auth Store -> Redirección) | 🔴 High |
| 07 | [**07-styling-system**](./07-styling-system/SKILL.md) | Design Tokens globales (variables) y abstracción de CSS global | 🟢 Low |
| 08 | [**08-state-management**](./08-state-management/SKILL.md) | Store Global (Pinia/Zustand) vs Elevamiento de Estado Local | 🔴 High |
| 09 | [**09-data-fetching**](./09-data-fetching/SKILL.md) | Repositorios externos e Interceptores HTTP (401 + Token Inject) | 🔴 High |
| 10 | [**10-advanced-navigation**](./10-advanced-navigation/SKILL.md) | Paginación por URL, Hero components y Breadcrumbs de navegación | 🟢 Low |
| 11 | [**11-baas-integration**](./11-baas-integration/SKILL.md) | Setup de BaaS, autenticación externa rápida y Database serverless | 🔴 High |
| 12 | [**12-route-guards**](./12-route-guards/SKILL.md) | Protección de rutas (Auth vs Guest) y redirecciones preventivas | 🟡 Med |

---

## 📁 Frontend Resources Index

These templates span the 4 major frameworks to assist the agent in adapting the pattern.

| Skill | Resource | Purpose |
|-------|----------|---------|
| 01 | [`env.template.md`](./01-project-setup/resources/env.template.md) | Variables de entorno según framework (`VITE_`, `PUBLIC_`, etc) |
| 01 | [`aliases.template.md`](./01-project-setup/resources/aliases.template.md) | Setup de TsConfig y Vite alias |
| 03 | [`lazy-routing.template.md`](./03-routing-strategy/resources/lazy-routing.template.md) | Configuración de nested routes y Lazy Componentes |
| 12 | [`guards.template.md`](./12-route-guards/resources/guards.template.md) | Middlewares frontend para Login/Protección |
| 08 | [`global-store.template.md`](./08-state-management/resources/global-store.template.md) | Zustand (React), Pinia (Vue), Signals (Angular), Nano(Astro) |
| 09 | [`interceptors.template.md`](./09-data-fetching/resources/interceptors.template.md) | Axios & HttpClient (Angular) inyectando JWT y echando al usuario |

---

## 🔁 Placeholder Convention

Use these universal placeholders to ask the agent to act on a domain.

| Placeholder | Meaning |
|-------------|---------|
| `{Framework}` | `React`, `Angular`, `Vue`, or `Astro` |
| `{FeatureName}` | Business Domain (e.g., `Invoice`, `UserProfile`) |
| `{ToasterLibrary}`| e.g. `sonner`, `vue-toastification`, `primeng` |
| `{API_URL}` | Real base url target `http://localhost:3000/api` |

---

> ⭐ Keep your UX consistent, your components dumb, and your tokens intercepted.
