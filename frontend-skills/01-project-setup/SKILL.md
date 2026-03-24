---
name: 01-project-setup
description: "Establishes the frontend foundation with strict typing, quality gates, environment hygiene, and portable delivery conventions."
risk: low
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
A strong frontend starts with predictable structure. This skill defines the minimum setup needed to keep imports clean, quality checks repeatable, configuration explicit, environment variables safe, and delivery rules understandable across modern frontend frameworks.

**Descripcion (ES):**
Un frontend solido empieza con una estructura predecible. Esta skill define la configuracion minima necesaria para mantener imports limpios, checks de calidad repetibles, configuracion explicita, variables de entorno seguras y reglas de entrega comprensibles en frameworks frontend modernos.

Related resources:
- [env.template.md](./resources/env.template.md)
- [aliases.template.md](./resources/aliases.template.md)
- [frontend-delivery-checklist.md](./resources/frontend-delivery-checklist.md)
- [frontend-deployment-strategy.md](./resources/frontend-deployment-strategy.md)

---

# 2. Skill Objective

**Objective (EN):**
Prepare a new or existing frontend project for maintainable development, predictable delivery checks, and portable deployment decisions across the chosen stack.
- Use this skill when: Bootstrapping a frontend app, cleaning inconsistent config, or standardizing imports, env files, and delivery commands.
- Do not use this skill when: You are only changing isolated component behavior with no impact on project configuration.

**Objetivo (ES):**
Preparar un proyecto frontend nuevo o existente para un desarrollo mantenible, con checks de entrega predecibles y decisiones de despliegue portables dentro del stack elegido.
- Use esta skill cuando: Inicialices una app frontend, limpies configuracion inconsistente o estandarices imports, archivos de entorno y comandos de entrega.
- No use esta skill cuando: Solo cambies el comportamiento de un componente aislado sin impacto en la configuracion del proyecto.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Frontend Runtime`: The chosen UI runtime and component model for the project.
2. `Tooling Layer`: The build, compile, test, and preview chain that resolves imports and environment values.
3. `Environment Rules`: Which values are public to the client, which remain server-only, and how hosting targets consume them.
4. `Quality Baseline`: Formatter, linter, type-check, build, preview, and optional deploy commands expected by the team.

**Entradas (ES):**
1. `Frontend Runtime`: El runtime UI y el modelo de componentes elegidos para el proyecto.
2. `Tooling Layer`: La cadena de build, compilacion, pruebas y preview que resuelve imports y variables de entorno.
3. `Environment Rules`: Que valores son publicos para el cliente, cuales deben permanecer del lado servidor y como los consumen los targets de hosting.
4. `Quality Baseline`: Formatter, linter, type-check, build, preview y comandos opcionales de deploy esperados por el equipo.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Strict compiler or type-checking configuration.
2. Stable alias configuration for top-level imports.
3. Safe `.env` and `.env.example` conventions adapted to the stack.
4. Baseline quality and delivery commands contributors can run before shipping changes.
5. A deployment strategy that distinguishes static, SPA, and hybrid targets clearly.

**Salidas (ES):**
1. Configuracion estricta del compilador o del type-checking.
2. Configuracion estable de aliases para imports de alto nivel.
3. Convenciones seguras de `.env` y `.env.example` adaptadas al stack.
4. Comandos base de calidad y entrega que los colaboradores puedan ejecutar antes de publicar cambios.
5. Una estrategia de despliegue que distinga con claridad entre targets estaticos, SPA e hibridos.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Enable strict development defaults:** Turn on strict typing or equivalent compiler checks whenever the stack supports it.
2. **Establish one quality gate vocabulary:** Keep formatter, linter, type-check, build, preview, and deploy-related commands obvious and stable so humans and agents can validate changes the same way every time.
3. **Create import aliases:** Define a stable alias such as `@/` for the main source folder and mirror that setup in the bundler, compiler, linter, and test runner.
4. **Separate public and private env values:** Only expose variables explicitly intended for the client bundle, and document the exposure rule per stack.
5. **Document the config contract:** Leave `.env.example`, alias docs, base scripts, and target-specific hosting notes clear enough for any contributor or agent to bootstrap the project safely.
6. **Choose delivery targets intentionally:** Identify whether the project ships as static files, SPA fallback hosting, or a hybrid/server runtime before wiring deployment commands.
7. **Keep the structure simple:** Prefer a clean root with source, config, quality scripts, and environment files over ad-hoc scattered setup.
8. **Adapt the pattern, not the literal example:** Rename files, layers, configs, and conventions to match the target project's framework, tooling, and business language.

**Instrucciones (ES):**
1. **Activa defaults estrictos de desarrollo:** Habilita tipado estricto o checks equivalentes del compilador siempre que el stack lo soporte.
2. **Establece un vocabulario unico de calidad:** Mantén formatter, linter, type-check, build, preview y comandos relacionados con deploy obvios y estables para que humanos y agentes validen cambios del mismo modo.
3. **Crea aliases de importacion:** Define un alias estable como `@/` para la carpeta principal de codigo y replica esa configuracion en bundler, compilador, linter y test runner.
4. **Separa variables publicas y privadas:** Expon al bundle cliente solo las variables pensadas para el navegador y documenta la regla por stack.
5. **Documenta el contrato de configuracion:** Deja `.env.example`, documentacion de aliases, scripts base y notas de hosting lo suficientemente claras para que cualquier colaborador o agente inicialice el proyecto con seguridad.
6. **Elige con intencion los targets de entrega:** Identifica si el proyecto se publica como archivos estaticos, hosting SPA con fallback o runtime hibrido/servidor antes de cablear comandos de despliegue.
7. **Mantén la estructura simple:** Prefiere una raiz limpia con codigo fuente, config, scripts de calidad y archivos de entorno en vez de una configuracion dispersa e improvisada.
8. **Adapta el patron, no el ejemplo literal:** Renombra archivos, capas, configuraciones y convenciones para ajustarlos al framework, tooling y lenguaje de negocio del proyecto objetivo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @01-project-setup to standardize the foundation of this frontend codebase.
1. Enable strict compiler checks, define reusable source aliases, and expose only client-safe environment values.
2. Leave formatter, linter, type-check, build, preview, and deploy-related commands clear for future contributors.
3. Document whether the project ships as static, SPA, or hybrid output before wiring deployment automation.
```

**Prompt (ES):**
```text
Usa la skill @01-project-setup para estandarizar la base de este proyecto frontend.
1. Activa checks estrictos del compilador, define aliases reutilizables y expone solo variables seguras para el cliente.
2. Deja claros los comandos de formatter, linter, type-check, build, preview y deploy para futuros colaboradores.
3. Documenta si el proyecto se publica como salida estatica, SPA o hibrida antes de automatizar el despliegue.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
{project-root}/
├── src/
├── .env.example
├── .gitignore
├── package.json or equivalent manifest
├── compiler config or equivalent
├── linter/formatter config or framework-equivalent config
├── build config or framework-equivalent config
└── README.md
```

## Adaptation Checklist / Lista de Adaptacion

**Checklist (EN):**
- [ ] Top-level imports resolve through a documented alias instead of deep relative paths.
- [ ] Public environment variables use the correct exposure mechanism for the chosen stack.
- [ ] Formatter, linter, type-check, build, preview, and deploy-related commands are easy to discover and run.
- [ ] Static, SPA, or hybrid delivery assumptions are documented before deployment automation is added.
- [ ] Contributors can clone the project and understand the base configuration quickly.
- [ ] Names, files, layers, configs, and conventions were adapted to the target project instead of copying the example structure literally.

**Checklist (ES):**
- [ ] Los imports de alto nivel se resuelven mediante un alias documentado en lugar de rutas relativas profundas.
- [ ] Las variables publicas usan el prefijo o mecanismo correcto de exposicion del framework.
- [ ] Los comandos de formatter, linter, type-check, build, preview y deploy son faciles de encontrar y ejecutar.
- [ ] Las suposiciones de entrega estatica, SPA o hibrida quedan documentadas antes de automatizar el despliegue.
- [ ] Cualquier colaborador puede clonar el proyecto y entender rapidamente su configuracion base.
- [ ] Los nombres, archivos, capas, configuraciones y convenciones se adaptaron al proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
