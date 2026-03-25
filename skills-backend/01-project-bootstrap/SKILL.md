---
name: 01-project-bootstrap
description: "Initializes a backend service with a clear entry point, environment-driven configuration, and a basic health contract."
risk: low
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Every backend needs a stable starting point before business logic is added. This skill sets up the application entry point, environment configuration, and a basic health contract so the service can boot, be verified quickly, and grow safely.

**Descripcion (ES):**
Todo backend necesita un punto de partida estable antes de agregar logica de negocio. Esta skill configura el punto de entrada de la aplicacion, la configuracion por entorno y un contrato basico de salud para que el servicio pueda arrancar, verificarse rapido y crecer con seguridad.

Related resources:
- [health-check.template.md](./resources/health-check.template.md)

---

# 2. Skill Objective

**Objective (EN):**
Create a minimal but professional backend bootstrap ready for future modules and adaptable to the target runtime, framework, and deployment style.
- Use this skill when: Starting a backend project, a microservice, or a new service runtime from scratch.
- Do not use this skill when: The project already has a working entry point and you are only extending existing features.

**Objetivo (ES):**
Crear un bootstrap backend minimo pero profesional, listo para modulos futuros y adaptable al runtime, framework y estilo de despliegue del proyecto objetivo.
- Use esta skill cuando: Inicies un backend, un microservicio o un nuevo runtime de servicio desde cero.
- No use esta skill cuando: El proyecto ya tenga un punto de entrada funcionando y solo estes extendiendo features existentes.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Runtime`: Node.js, Python, Java, Go, .NET, or another server runtime.
2. `HTTP Layer`: Native framework, standard library server, or equivalent transport adapter.
3. `Environment Values`: `PORT`, environment name, and required startup config.

**Entradas (ES):**
1. `Runtime`: Node.js, Python, Java, Go, .NET u otro runtime de servidor.
2. `HTTP Layer`: Framework web, servidor de libreria estandar o adaptador equivalente de transporte.
3. `Environment Values`: `PORT`, nombre del entorno y configuracion necesaria para arrancar.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. A working application entry point.
2. A basic liveness endpoint such as `GET /health`.
3. Environment templates and startup defaults that are safe to version.

**Salidas (ES):**
1. Un punto de entrada de aplicacion funcionando.
2. Un endpoint basico de liveness como `GET /health`.
3. Plantillas de entorno y defaults de arranque seguros para versionar.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Initialize the project runtime:** Create the base package, module, or workspace using the ecosystem's standard tooling.
2. **Add only the essential HTTP dependencies:** Keep bootstrap minimal until real feature needs appear.
3. **Create a clear entry point:** Read configuration from environment, start the HTTP server, and register a simple health route.
4. **Define safe defaults:** Fall back to a standard port like `8080` and expose the expected environment variables in `.env.example`.
5. **Protect local secrets:** Keep real `.env` files out of version control and commit only templates or examples.
6. **Leave deeper readiness checks for the deployment layer:** Bootstrap should prove the service starts cleanly; production orchestration can add dependency-aware readiness later.
7. **Adapt the pattern, not the literal example:** Rename files, layers, contracts, and integrations to match the target project's architecture, framework conventions, and business language.

**Instrucciones (ES):**
1. **Inicializa el runtime del proyecto:** Crea el paquete, modulo o workspace base usando el tooling estandar del ecosistema.
2. **Agrega solo las dependencias HTTP esenciales:** Mantén el bootstrap minimo hasta que existan necesidades reales de features.
3. **Crea un punto de entrada claro:** Lee configuracion desde el entorno, inicia el servidor HTTP y registra una ruta simple de salud.
4. **Define defaults seguros:** Usa un puerto estandar como `8080` cuando no haya configuracion explicita y expone las variables esperadas en `.env.example`.
5. **Protege secretos locales:** Mantén los `.env` reales fuera del control de versiones y sube solo plantillas o ejemplos.
6. **Deja los readiness checks profundos para la capa de despliegue:** El bootstrap debe demostrar que el servicio arranca limpio; la orquestacion de produccion puede agregar chequeos con dependencias despues.
7. **Adapta el patron, no el ejemplo literal:** Renombra archivos, capas, contratos e integraciones para ajustarlos a la arquitectura, las convenciones del framework y el lenguaje de negocio del proyecto objetivo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @01-project-bootstrap to initialize a new `{Runtime}` backend service.
1. Create a clear entry point that reads environment config and starts the HTTP layer.
2. Add a basic `GET /health` endpoint plus safe environment templates for local development.
```

**Prompt (ES):**
```text
Usa la skill @01-project-bootstrap para inicializar un nuevo servicio backend en `{Runtime}`.
1. Crea un punto de entrada claro que lea configuracion del entorno y levante la capa HTTP.
2. Agrega un endpoint basico `GET /health` y plantillas seguras de entorno para desarrollo local.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
{project-root}/
├── .env.example
├── {source-root}/
│   ├── {entry-point}.{ext}
│   ├── {app-bootstrap}.{ext}
│   └── health/
│       └── health-endpoint.{ext}
└── {config-root}/
    └── runtime-config.{ext}
```

## Adaptation Checklist / Lista de Adaptacion

**Checklist (EN):**
- [ ] The service starts from a single clear entry point.
- [ ] `GET /health` returns a successful response when the process is alive.
- [ ] Real local secrets are excluded from version control.
- [ ] Bootstrap remains small and leaves deeper operational checks to the deployment layer.
- [ ] Names, files, layers, and integrations were adapted to the target project's conventions instead of copying the example structure literally.

**Checklist (ES):**
- [ ] El servicio arranca desde un punto de entrada unico y claro.
- [ ] `GET /health` devuelve una respuesta exitosa cuando el proceso esta vivo.
- [ ] Los secretos locales reales estan excluidos del control de versiones.
- [ ] El bootstrap se mantiene pequeno y deja los chequeos operativos profundos para la capa de despliegue.
- [ ] Los nombres, archivos, capas e integraciones se adaptaron a las convenciones del proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
