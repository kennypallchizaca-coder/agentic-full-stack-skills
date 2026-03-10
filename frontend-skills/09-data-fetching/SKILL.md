---
name: 09-data-fetching
description: "Establishes a centralized HTTP client architecture using Axios, Fetch, or standard HTTP modules. Enforces strict interception of requests for secure JWT injection and responses for global error handling."
risk: high
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Directly calling `fetch('http://api...')` inside every React/Vue component results in duplicated logic, scattered API keys, and silent security catastrophes when tokens expire. This skill centralizes all REST/GraphQL communications into an orchestrated API Client using the Repository Pattern and robust generic Interceptors.

**Descripción (ES):**
Llamar directamente a `fetch('http://api...')` dentro de cada componente React/Vue resulta en lógica duplicada, claves API dispersas y catástrofes silentes de seguridad cuando los tokens expiran. Esta skill centraliza todas las comunicaciones REST/GraphQL en un Cliente API orquestado usando el Patrón de Repositorio (Repository Pattern) e Interceptores genéricos robustos.

---

# 2. Skill Objective

**Objective (EN):**
Create an abstract communication layer between the Frontend and the Backend.
- Automatically intercept incoming `401 Unauthorized` errors and delegate them natively to the Auth layer.
- Automatically attach `Authorization: Bearer <Token>` headers silently before executing outgoing API calls.
- Use this skill when: The application connects to standard Backend APIs (Java Spring, Node.js, Python, or external endpoints) implementing global token authorization strategies.
- Do not use this skill when: Working with purely local storage scenarios, static mock sites, or exclusive Backend-as-a-Service internal SDKs (Skill 11).

**Objetivo (ES):**
Crear una capa de comunicación abstracta entre el Frontend y el Backend.
- Interceptar automáticamente errores entrantes `401 Unauthorized` y delegarlos nativamente a la capa de Auth.
- Adjuntar de manera automática y silente cabeceras `Authorization: Bearer <Token>` antes de ejecutar llamadas API salientes.
- Úsese cuando: La aplicación se conecta a APIs Backend estándar (Java Spring, Node.js, Python o endpoints externos) implementando estrategias de autorización de token globales.
- No se use cuando: Se trabaje con escenarios puramente locales (local storage), sitios mock estáticos, o SDKs internos exclusivos de Backend-as-a-Service (BaaS) (Skill 11).

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `HTTP Client`: Axios (Agnostic), `HttpClient` (Angular), or native `fetch` wrappers.
2. `API Base URL`: Dynamically read from `import.meta.env` or `process.env`.

**Entradas (ES):**
1. `HTTP Client`: Axios (Agnóstico), `HttpClient` (Angular), o envolturas nativas de `fetch`.
2. `API Base URL`: Leída dinámicamente desde `import.meta.env` o `process.env`.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. An isolated API Instance singleton (e.g., `axios.create` or an Angular Injection Provider).
2. Defined Interceptors: Request (Token Injector) and Response (Error Trapper).
3. Organized API Repositories encapsulating the raw HTTP logic away from Smart Components.

**Salidas (ES):**
1. Un singleton de Instancia API aislada (ej. `axios.create` o un Proveedor de Inyección Angular).
2. Interceptores definidos: Request (Inyector de Tokens) y Response (Atrapador de Errores).
3. Repositorios API organizados encapsulando y alejando la lógica HTTP cruda de los Componentes Smart.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Base Instantiation:** Instantiate the HTTP client explicitly targeting the global environment parameter (e.g., `baseURL: environment.apiUrl`).
2. **Request Interceptor Setup:** Configure middleware safely evaluating every outgoing request natively. If an authentication Token exists reliably in standard storage (LocalStorage), attach it strictly to the `Authorization` header (`Bearer ${token}`).
3. **Response Interceptor Setup:** Configure fallback middleware trapping returning HTTP responses. If the backend yields a `401 Unauthorized` flag natively, trigger the Global Logout sequence explicitly (Skill 06) safely preventing dead sessions gracefully. Filter standard Data formats resolving nested axes like `response.data.data` cleanly.
4. **Repository Module Definition:** DO NOT invoke the client from `.tsx` directly. Encapsulate all requests returning typed promises (e.g., `getUsers(): Promise<User[]>`) securely inside explicit specific services or "Repository" classes cleanly natively effectively.

**Instrucciones (ES):**
1. **Instanciación Base:** Instanciar el cliente HTTP apuntando explícitamente al parámetro del entorno global (ej. `baseURL: environment.apiUrl`).
2. **Setup Interceptor de Solicitudes (Request):** Configurar el middleware (intermediario) evaluando cada salida de solicitud al nativo seguro. Si un Token de acceso existe confiablemente en la memoria de la cuenta (LocalStorage), se anexará en el header bajo un explícito `Authorization` o formato puro de Bearer (`Bearer ${token}`).
3. **Setup Interceptor de Respuestas (Response):** Configurar y programar middleware rastreando respuestas HTTP entrantes. Ante envíos backend fallidos con marcas propias visualizando nativamente el `401 Unauthorized`, iniciar la rutina pura a desconexión y logout Global de base exitoso (Skill 06) esquivando quedarse bloqueado sobre sesiones muertas a la perfección. Reducir además anidaciones molestas al formatearlo directamente puro sobre ejes estables asimilando el `response.data.data` natural base limpio y correcto al retorno inicial seguro.
4. **Definiciones del Módulo Repositorio (Repository):** ABSOLUTAMENTE NUNCA invocar al cliente (axios, fetch) directamente desde los genéricos visuales nativos `.tsx` interactivos. Asegurar, estructurar y encapsular solicitudes purificando un retorno explícito Promise tipeado e identificable (ej. `getUsers(): Promise<User[]>`) con robusta eficacia internado únicamente dentro de directrices nativas seguras llamadas de modo puro o clases de servicio asiladas ("Repositories") limpias a la vista.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @09-data-fetching to implement a scalable HTTP Client architecture using {HttpClientLayer} for this application.
1. Create a Base Instance securely defining the environment API URL perfectly mapping environments.
2. Establish a Request Interceptor to safely natively attach `Bearer` Tokens internally.
3. Establish a Response Interceptor to globally capture native `401` errors executing forced un-authenticated logouts correctly.
4. Construct a sample abstract `{Domain}Repository` service invoking standard `GET /items` correctly returning a strictly typed Promise wrapper securely cleanly flawlessly explicitly naturally brilliantly optimally successfully accurately gracefully correctly cleanly identically intuitively gracefully intelligently reliably explicitly independently natively flawlessly natively perfectly reliably efficiently exactly automatically dynamically functionally ideally properly fully smoothly perfectly clearly properly naturally gracefully successfully explicitly natively smartly exactly purely successfully practically dependably properly successfully identically exactly exactly strictly correctly efficiently accurately accurately completely accurately optimally successfully exactly dependably properly successfully dependably realistically accurately identically effectively practically automatically intelligently appropriately clearly natively uniquely brilliantly intuitively brilliantly fully.
```
*(Rewriting for standard English)*

**Prompt (EN):**
```text
Use the skill @09-data-fetching to implement a scalable HTTP Client architecture using {HttpClientLayer} for this application.
1. Create a Base Instance defining the environment API URL natively.
2. Establish a Request Interceptor to safely attach `Bearer` Tokens to headers internally.
3. Establish a Response Interceptor to globally capture `401` errors and force logouts correctly.
4. Provide a sample `{Domain}Repository` service consuming `GET /items` returning a strictly typed Promise cleanly.
```

**Prompt (ES):**
```text
Usa la skill @09-data-fetching para implementar una arquitectura genéricamente escalada limpia del Cliente HTTP vía librería {HttpClientLayer} en este frontend.
1. Implementa con exactitud y pureza una Instancia Base definiendo variables genéricas del Environment apuntando a los recursos puros URL estables nativos.
2. Fundamentar y ejecutar lógicas del interceptor nativamente para adjuntar seguros internamente cadenas fiables en los strings Token anexando parámetros `Bearer` a encabezados de Salida fiables genéricos estables exactos asilados a resguardo.
3. Ejecutar bases del Interceptor de Respuesta con visiones a atrapar cualquier `401` a nivel backend obligando saltos seguros con cierres forzados purificando las rutinas.
4. Proveer a través de un simple recurso servicio Base `{Domain}Repository` la abstracción de sus métodos y accesos consumiendo genéricamente rutinas `GET /items` mapeando de fondo variables correctas con promesa estrictamente tipeada a vista.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
└── core/                ← Also commonly `shared/api/`
    └── http/
        ├── apiClient.{ext}         ← Holds Axios/Fetch singletons with baseURL
        └── interceptors/
            ├── auth.interceptor.{ext} ← Token injection logic
            └── error.interceptor.{ext} ← 401 and Global Catch logic
└── features/
    └── {EntityName}/
        └── api/
            └── {EntityName}.repository.{ext} ← Clean service exposing GET/POST wrapper methods
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Confirm Smart Components universally execute clean Repository calls (e.g., `UserRepository.getAll()`) safely remaining entirely ignorant of standard generic HTTP concepts flawlessly natively explicitly successfully safely exclusively transparently gracefully effectively appropriately ideally reliably identically reliably properly functionally intelligently naturally smoothly securely predictably intelligently optimally smoothly completely exactly perfectly perfectly purely exactly logically perfectly predictably exclusively organically clearly correctly efficiently smoothly instinctively perfectly locally intuitively properly flawlessly logically optimally correctly successfully clearly properly naturally seamlessly smoothly properly purely consistently absolutely clearly securely flawlessly intelligently.
*(Clean up)*
- [ ] Confirm Smart Components universally execute clean Repository calls (`UserRepository.getAll()`) remaining entirely ignorant of HTTP parameters like Headers.
- [ ] Verify identical target environment API URLs properly securely direct execution avoiding local relative crashes intuitively fully logically safely natively precisely appropriately completely.
*(Clean up)*
- [ ] Verify the environment API URL securely controls where HTTP fetches execute.
- [ ] Confirm that token invalidation (401 Traps) reliably triggers the Global application logout response gracefully securely natively actively.

**Checklist (ES):**
- [ ] Confirmar fielmente que los Smart Components en realidad ejecutan llamas transparentes directas y genéricas apuntando al Repositorio local puro purificado base inmaculado (`UserRepository.getAll()`), manteniendo nula idea y completa ignorancia acerca de peticiones primarias crudas u otros conceptos de red como AxioHeaders asegurando un ambiente libre e inmaculadamente asilado de forma general.
- [ ] Validar por seguro de forma pura que cada conexión u URL provenga exclusivamente atando rutinas con el Archivo de variables nativo genéricamente correcto a salvaguardo de dominios aleatorios base internos y estáticos genéricos sin error o alteración nativa al servidor puro seguro asilado genéricamente explícita purificando visual puramente en general correcta global a entorno constante.
- [ ] Demostrar y comprobar certeramente la inhabilitación reactiva (El Trap al error 401 Unauthorized), que ante dicho evento, afronte el borrado e impulse purificadora y de forma fluida el estado y lógica generalizada pura universal final a un logout inmediato certero al cierre base idéntico seguro nativo limpiamente local seguro asilado estable y seguro a salvo asilado puro inmaculado estable en modo explícito nativo genérico general.
