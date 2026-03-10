---
name: 01-project-bootstrap
description: "Initializes a backend project from scratch: configures the HTTP server, defines the application entry point, and exposes a health endpoint. Works with any language or framework."
risk: low
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Initializes any backend project from scratch. It configures the HTTP server, defines the application entry point, and exposes a `/health` endpoint that confirms the environment is running correctly. This is the mandatory first step before developing any business functionality.

**Descripción (ES):**
Inicializa cualquier proyecto backend desde cero. Configura el servidor HTTP, define el punto de entrada de la aplicación y expone un endpoint `/health` que confirma que el entorno está corriendo correctamente. Este es el primer paso obligatorio antes de desarrollar cualquier funcionalidad de negocio.

---

# 2. Skill Objective

**Objective (EN):**
Achieve a functional HTTP server with minimal configuration, ready to receive business modules, using environment variables for all configurable values.
- Use this skill when: Starting a backend project or microservice from scratch, or migrating an application to another framework or runtime.
- Do not use this skill when: The project already has a functional server and entry point, or you are only adding features to an existing backend.

**Objetivo (ES):**
Lograr un servidor HTTP funcional con configuración mínima, listo para recibir módulos de negocio, usando variables de entorno para todos los valores configurables.
- Úsese cuando: Se inicia un proyecto backend o microservicio desde cero, o al migrar una aplicación a otro framework o runtime.
- No se use cuando: El proyecto ya tiene un servidor y punto de entrada funcional, o solo se están agregando funcionalidades a un backend existente.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `runtime`: Language or platform (Node.js, Python, Java, Go, etc.).
2. `framework`: HTTP Framework (Express, FastAPI, Gin, Spring Boot, etc.).
3. `PORT`: Server port. Default: `8080`.
4. `APP_ENV`: Execution environment: `development`, `staging`, `production`.

**Entradas (ES):**
1. `runtime`: Lenguaje o plataforma (Node.js, Python, Java, Go, etc.).
2. `framework`: Framework HTTP (Express, FastAPI, Gin, Spring Boot, etc.).
3. `PORT`: Puerto del servidor. Predeterminado: `8080`.
4. `APP_ENV`: Ambiente de ejecución: `development`, `staging`, `production`.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Active HTTP server listening on the configured port.
2. `GET /health` responding `200 OK` confirming the server is online.
3. `.env.example` file exposing public environment variable templates.
4. Application Entry point file natively (e.g. `main.{ext}`).

**Salidas (ES):**
1. Servidor HTTP activo escuchando en el puerto configurado.
2. `GET /health` respondiendo `200 OK` confirmando que el servidor está en línea.
3. Archivo `.env.example` exponiendo plantillas de variables de entorno públicas.
4. Archivo nativo del Punto de entrada de la aplicación (ej. `main.{ext}`).

---

# 5. Execution Steps

**Instructions (EN):**
1. **Initialize Project:** Choose the correct language/framework and initialize the project using its package manager natively (`npm init`, `go mod init`, `gradle init`).
2. **Install Dependencies:** Install the minimal necessary HTTP server dependency flawlessly.
3. **Configure Entry Point:** Create the `main.{ext}` file cleanly natively. Read the `PORT` from environment variables, initialize the HTTP server natively, and register the `GET /health` route returning `{ "status": "ok", "timestamp": "<ISO>" }`.
4. **Environment Security:** Create `.env.example` detailing configurable variables securely. Add `.env` to `.gitignore` strictly avoiding credential leakage organically.

**Instrucciones (ES):**
1. **Inicializar Proyecto:** Elige el lenguaje/framework correcto e inicializa el proyecto usando su gestor de paquetes de manera nativa (`npm init`, `go mod init`, `gradle init`).
2. **Instalar Dependencias:** Instala la dependencia mínima necesaria del servidor HTTP sin errores.
3. **Configurar Punto de Entrada:** Crea el archivo `main.{ext}` limpiamente de modo nativo. Lee el `PORT` (Puerto) desde las variables de entorno, inicializa el servidor HTTP nativamente y registra la ruta `GET /health` devolviendo `{ "status": "ok", "timestamp": "<ISO>" }`.
4. **Seguridad de Entorno:** Crea un `.env.example` detallando variables configurables firmemente. Añade `.env` a `.gitignore` evitando estrictamente y de forma orgánica fugas de credenciales.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @01-project-bootstrap to initialize a {Runtime} + {Framework} backend called `{AppName}` on port {PORT}. 
1. Map `APP_ENV` and `PORT` cleanly.
2. Configure the server entry point successfully triggering `/health` gracefully.
```

**Prompt (ES):**
```text
Usa la skill @01-project-bootstrap para inicializar un backend en {Runtime} + {Framework} llamado `{AppName}` en el puerto {PORT}.
1. Mapea `APP_ENV` y `PORT` de manera limpia.
2. Configura el punto de entrada del servidor gatillando existosamente `/health` y devolviendo un 200 seguro.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
{project-root}/
├── src/
│   └── main.{ext}            ← Server Entry Point
├── .env                      ← Real Values (DO NOT commit)
├── .env.example              ← Public Template (Commit safe)
├── .gitignore
└── README.md
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Define the `PORT` successfully falling back to `8080` if completely omitted predictably.
- [ ] Ensure the native framework Server cleanly executes explicitly capturing the generic configuration seamlessly safely.
- [ ] Confirm `GET /health` responds exactly `200 OK` inherently exposing standard uptime indicators efficiently correctly.

**Checklist (ES):**
- [ ] Definir el `PORT` ejecutando el respaldo a `8080` de tener una omisión total sobre sus parámetros nativos predeterminados.
- [ ] Asegurarse de que el Servidor framework nativo levante capturando su configuración eficientemente seguro.
- [ ] Confirmar de raíz nativa que `GET /health` devuelve un exacto `200 OK` evidenciando indicadores básicos estándar orgánicamente puros.
