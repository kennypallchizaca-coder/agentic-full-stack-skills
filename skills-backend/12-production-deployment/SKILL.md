---
name: 12-production-deployment
description: "Hardens backend delivery for production with reproducible builds, secret-safe runtime config, observability, release gates, and rollback discipline."
risk: high
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Production readiness is not just "it runs on my machine." This skill defines how to package, configure, release, and operate a backend with secure runtime settings, health checks, structured logs, monitoring hooks, CI/CD guardrails, and rollback awareness.

**Descripción (ES):**
Estar listo para producción no es solo "corre en mi maquina". Esta skill define como empaquetar, configurar, liberar y operar un backend con runtime seguro, health checks, logs estructurados, ganchos de monitoreo, guardrails de CI/CD y criterio de rollback.

Related resources:
- [edge-runtime.matrix.md](./resources/edge-runtime.matrix.md)
- [observability-release-checklist.md](./resources/observability-release-checklist.md)
- [process-supervision.template.md](./resources/process-supervision.template.md)
- [reverse-proxy.template.md](./resources/reverse-proxy.template.md)
- [release-pipeline.template.md](./resources/release-pipeline.template.md)

---

# 2. Skill Objective

**Objective (EN):**
Prepare the backend for secure, repeatable deployment across staging and production environments, regardless of runtime, hosting model, or process manager.
- Use this skill when: Building Docker images, creating deployment manifests, configuring reverse proxies, or defining release pipelines.
- Do not use this skill when: You only need a local dev script with no operational or release requirements.

**Objetivo (ES):**
Preparar el backend para un despliegue seguro y repetible en staging y producción, sin depender del runtime, modelo de hosting o process manager.
- Úsese cuando: Construyas imágenes Docker, manifiestos de despliegue, configuraciónes de reverse proxy o pipelines de release.
- No se use cuando: Solo necesites un script de desarrollo local sin requerimientos operativos ni de release.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Runtime Target`: Container platform, VM, PaaS, serverless runtime, or orchestrator.
2. `Build Artifacts`: JAR, compiled Node app, Python package, Go binary, or equivalent release output.
3. `Operational Requirements`: Secrets, health/readiness checks, logs, metrics, migrations, backups, and rollback expectations.

**Entradas (ES):**
1. `Runtime Target`: Plataforma de contenedores, VM, PaaS, runtime serverless u orquestador.
2. `Build Artifacts`: JAR, app Node compilada, paquete Python, binario Go o salida equivalente de release.
3. `Operational Requirements`: Secretos, health/readiness, logs, métricas, migraciones, backups y expectativas de rollback.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. A production-focused Dockerfile, service manifest, or native process configuration.
2. Safe runtime configuration driven by environment variables or secret stores.
3. Operational hooks for liveness/readiness, structured logs, metrics, and smoke checks.
4. Release guardrails covering migrations, deployment válidation, and rollback criteria.

**Salidas (ES):**
1. Un Dockerfile, manifiesto de servicio o configuración de proceso nativo orientado a producción.
2. Configuracion segura de runtime impulsada por variables de entorno o secret stores.
3. Ganchos operativos para liveness/readiness, logs estructurados, métricas y smoke checks.
4. Guardrails de release que cubran migraciones, válidación del despliegue y criterios de rollback.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Choose the delivery model intentionally:** Native Linux service, PM2, Docker Compose, Kubernetes, or PaaS should match the project scale and operational maturity.
2. **Create a reproducible build:** Build the release artifact deterministically. If you ship containers, prefer multi-stage builds to keep compilers and dev tooling out of the runtime image.
3. **Run with least privilege:** Use a non-root runtime user whenever possible and keep the final image or server process as small as practical.
4. **Externalize runtime configuration:** Load database URLs, JWT secrets, API keys, ports, and environment-specific toggles from env vars or a secret manager, never from committed local files.
5. **Separate liveness from readiness when the platform supports it:** A lightweight process-alive check can differ from a dependency-aware readiness check used by orchestrators or load balancers.
6. **Expose operational visibility:** Emit structured logs, stable health output, and metrics or tracing hooks that allow monitoring systems to detect failures quickly.
7. **Harden the internet-facing edge:** If the backend is public, terminate HTTPS, set security headers, and apply rate limiting or reverse-proxy protections where appropriate.
8. **Treat migrations as release steps:** Run schema changes deliberately, verify compatibility, and avoid deploys that require manual guesswork in production.
9. **Add release gates:** CI/CD should build, test, package, deploy, and run smoke checks before declaring success.
10. **Define rollback criteria before deployment:** Know what signals trigger rollback, how to revert the previous version, and how to protect data consistency if the release fails.
11. **Adapt the pattern, not the literal example:** Rename files, layers, manifests, and operational tooling to fit the target architecture and platform conventions.

**Instrucciones (ES):**
1. **Elige el modelo de entrega con intención:** Servicio nativo Linux, PM2, Docker Compose, Kubernetes o PaaS deben corresponder al tamano del proyecto y a su madurez operativa.
2. **Crea un build reproducible:** Genera el artefacto de release de forma determinista. Si entregas contenedores, prefiere builds multi-stage para dejar compiladores y tooling de desarrollo fuera del runtime.
3. **Corre con mínimo privilegio:** Usa un usuario no root cuando sea posible y mantén la imagen final o el proceso del servidor tan pequeño como sea practico.
4. **Externaliza la configuración de runtime:** Carga URLs de base, secretos JWT, API keys, puertos y toggles por entorno desde env vars o un secret manager, nunca desde archivos locales versionados.
5. **Separa liveness de readiness cuando la plataforma lo soporte:** Un chequeo ligero de proceso vivo puede diferir de un chequeo de disponibilidad con dependencias usado por orquestadores o balanceadores.
6. **Expone visibilidad operativa:** Emite logs estructurados, salida de salud estable y métricas o hooks de tracing que permitan detectar fallos rápido.
7. **Endurece el borde expuesto a internet:** Si el backend es público, termina HTTPS, configura security headers y aplica rate limiting o protecciónes de reverse proxy cuando corresponda.
8. **Trata las migraciones como pasos de release:** Ejecuta cambios de esquema con intención, verifica compatibilidad y evita deploys que requieran adivinacion manual en producción.
9. **Agrega release gates:** CI/CD debe build, test, empaquetar, desplegar y correr smoke checks antes de declarar éxito.
10. **Define criterios de rollback antes del despliegue:** Debes saber que señales disparan rollback, como volver a la version previa y como proteger consistencia de datos si el release falla.
11. **Adapta el patrón, no el ejemplo literal:** Renombra archivos, capas, manifiestos y tooling operativo para encajar con la arquitectura y las convenciones de la plataforma objetivo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @12-production-deployment to harden this backend for production.
1. Package the app with secure runtime config, health/readiness checks, and structured logs.
2. Define release gates, smoke tests, and rollback criteria for the chosen hosting model.
```

**Prompt (ES):**
```text
Usa la skill @12-production-deployment para endurecer este backend para producción.
1. Empaqueta la app con configuración segura de runtime, health/readiness y logs estructurados.
2. Define release gates, smoke tests y criterios de rollback para el hosting elegido.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
{project-root}/
├── Dockerfile (optional)
├── .dockerignore (optional)
├── compose.yaml (optional)
├── .github/
│   └── workflows/
│       └── deploy.{yml|yaml}
├── deploy/
│   ├── service-manifest.{yml|yaml|json}
│   ├── edge/
│   │   └── reverse-proxy.{conf|toml|json}
│   ├── process/
│   │   └── supervisor.{service|conf|json}
│   └── scripts/
│       ├── migrate.{sh|ps1}
│       ├── smoke-check.{sh|ps1}
│       └── rollback.{sh|ps1}
├── ops/
│   └── runbooks/
│       └── release-checklist.md
└── src/
    └── health/
        └── health-endpoint.{ext}
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] The release artifact is reproducible and excludes dev-only tooling and secrets.
- [ ] The runtime runs with least privilege whenever the platform allows it.
- [ ] Production config comes from environment or secret stores, not committed local files.
- [ ] Health, readiness, logs, and metrics exist in a form the platform can observe.
- [ ] CI/CD or release scripts include build, test, deploy, and smoke válidation steps.
- [ ] Rollback criteria and migration discipline are defined before shipping.
- [ ] Internet-facing deployments use HTTPS and appropriate edge protections.
- [ ] Names, files, layers, manifests, and tooling were adapted to the target project's conventions instead of copying the example structure literally.

**Checklist (ES):**
- [ ] El artefacto de release es reproducible y excluye tooling de desarrollo y secretos.
- [ ] El runtime corre con mínimo privilegio siempre que la plataforma lo permita.
- [ ] La configuración de producción viene del entorno o de secret stores, no de archivos locales versionados.
- [ ] Existen health, readiness, logs y métricas en una forma observable por la plataforma.
- [ ] CI/CD o los scripts de release incluyen pasos de build, test, deploy y smoke válidation.
- [ ] Los criterios de rollback y la disciplina de migraciones se definen antes de publicar.
- [ ] Los despliegues expuestos a internet usan HTTPS y protecciónes adecuadas en el borde.
- [ ] Los nombres, archivos, capas, manifiestos y tooling se adaptaron a las convenciones del proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
