---
name: 04-service-layer
description: "Moves business rules out of controllers into services so use cases stay reusable, testable, and independent from HTTP details."
risk: low
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Controllers should handle transport concerns, not business decisions. This skill defines a service layer where validations, workflows, calculations, and orchestration live behind a clean use-case boundary with explicit dependency injection and test seams.

**Descripcion (ES):**
Los controladores deben manejar transporte, no decisiones de negocio. Esta skill define una capa de servicios donde validaciones, flujos, calculos y orquestacion viven detras de un limite limpio de caso de uso, con inyeccion de dependencias explicita y puntos claros para pruebas.

Related resources:
- [service-interface.template.md](./resources/service-interface.template.md)
- [service-test-strategy.md](./resources/service-test-strategy.md)

---

# 2. Skill Objective

**Objective (EN):**
Create services that encapsulate business logic and remain reusable across controllers, jobs, tests, message consumers, and framework styles.
- Use this skill when: Logic is growing beyond request parsing, or multiple endpoints share the same business workflow.
- Do not use this skill when: The change is limited to transport metadata or a trivial pass-through with no business behavior.

**Objetivo (ES):**
Crear servicios que encapsulen logica de negocio y puedan reutilizarse entre controladores, jobs, pruebas, consumidores de mensajes y distintos estilos de framework.
- Use esta skill cuando: La logica ya supera el parseo de requests o varios endpoints comparten el mismo flujo de negocio.
- No use esta skill cuando: El cambio se limita a metadatos de transporte o a un passthrough trivial sin comportamiento de negocio.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Use Case`: The business action to implement, such as creating an order or approving a payment.
2. `Dependencies`: Repositories, gateways, queues, caches, or external services required by the flow.
3. `Domain Rules`: Validations, invariants, permissions, calculations, and side effects.

**Entradas (ES):**
1. `Use Case`: La accion de negocio a implementar, como crear una orden o aprobar un pago.
2. `Dependencies`: Repositorios, gateways, colas, caches o servicios externos requeridos por el flujo.
3. `Domain Rules`: Validaciones, invariantes, permisos, calculos y efectos secundarios.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. A thin controller or transport adapter that only translates input/output.
2. A service contract and implementation when the project benefits from explicit interfaces, or at least a clearly isolated service boundary.
3. Business rules that can be unit-tested without booting an HTTP server.
4. Clear dependency injection wiring for repositories and external integrations.

**Salidas (ES):**
1. Un controlador o adaptador de transporte delgado que solo traduzca entrada/salida.
2. Un contrato de servicio y su implementacion cuando el proyecto se beneficie de interfaces explicitas, o al menos un limite de servicio claramente aislado.
3. Reglas de negocio que puedan probarse sin levantar un servidor HTTP.
4. Wiring claro de inyeccion de dependencias para repositorios e integraciones externas.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Keep controllers thin:** Parse route/query/body input, call the service, and map the result back to HTTP or another transport.
2. **Inject dependencies explicitly:** Use constructor injection or the framework equivalent so repositories and clients are visible, replaceable, and easy to mock.
3. **Centralize business rules in the service:** Validations, calculations, permission checks, orchestration, and workflow branching belong here instead of in controllers.
4. **Keep transport objects out of the core use case:** Services should accept DTOs or plain arguments, not raw `Request`, `Response`, or framework-specific controller context.
5. **Let services coordinate repositories:** Controllers should not talk directly to persistence or external gateways when a use case is involved.
6. **Raise meaningful domain errors:** Throw or return business-level errors that the global error layer can translate into HTTP responses or queue outcomes.
7. **Design for reuse beyond HTTP:** A service method should remain callable from jobs, schedulers, queue consumers, CLI commands, or tests.
8. **Create a deliberate test seam:** Unit-test happy paths, validation failures, dependency failures, and branching rules with mocks, fakes, or test doubles.
9. **Use interfaces when they help the codebase:** If the project standard uses Interface + Implementation, keep controllers coupled to the contract. In smaller codebases, a single service class is acceptable if the boundary is still clean and testable.
10. **Adapt the pattern, not the literal example:** Rename files, layers, contracts, and integrations to match the target project's architecture, framework conventions, and business language.

**Instrucciones (ES):**
1. **Mantén los controladores delgados:** Parsea `route/query/body`, llama al servicio y mapea el resultado de vuelta a HTTP u otro transporte.
2. **Inyecta dependencias de forma explicita:** Usa constructor injection o el equivalente del framework para que repositorios y clientes sean visibles, reemplazables y faciles de mockear.
3. **Centraliza las reglas de negocio en el servicio:** Validaciones, calculos, chequeos de permiso, orquestacion y ramas del flujo deben vivir aqui y no en los controladores.
4. **Mantén los objetos de transporte fuera del caso de uso:** Los servicios deben recibir DTOs o argumentos planos, no objetos crudos como `Request`, `Response` o contexto del framework.
5. **Deja que los servicios coordinen repositorios:** Los controladores no deben hablar directo con persistencia ni con gateways externos cuando hay un caso de uso de por medio.
6. **Lanza errores de dominio con significado:** Emite errores de negocio que la capa global de errores pueda traducir a respuestas HTTP o resultados de cola.
7. **Disena para reutilizar mas alla de HTTP:** Un metodo de servicio debe poder usarse desde jobs, schedulers, consumidores de colas, comandos CLI o pruebas.
8. **Crea un punto de prueba deliberado:** Prueba happy paths, fallos de validacion, fallos de dependencias y ramas de negocio con mocks, fakes o test doubles.
9. **Usa interfaces cuando ayuden al codebase:** Si el proyecto estandariza Interface + Implementation, mantén los controladores acoplados al contrato. En codebases pequenos, una sola clase de servicio es valida si el limite sigue limpio y testeable.
10. **Adapta el patron, no el ejemplo literal:** Renombra archivos, capas, contratos e integraciones para ajustarlos a la arquitectura, las convenciones del framework y el lenguaje de negocio del proyecto objetivo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @04-service-layer to implement the `{UseCase}` workflow.
1. Keep the controller limited to transport mapping and move business rules into a reusable service.
2. Add a test plan for success, validation failure, and dependency failure branches.
```

**Prompt (ES):**
```text
Usa la skill @04-service-layer para implementar el flujo `{UseCase}`.
1. Deja el controlador limitado al mapeo de transporte y mueve las reglas de negocio a un servicio reutilizable.
2. Agrega un plan de pruebas para ramas de exito, fallo de validacion y fallo de dependencias.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
└── modules/
    └── {feature}/
        ├── dto/
        ├── {feature}.controller.{ext}
        ├── application/
        │   ├── {feature}.service.{ext}
        │   └── {feature}.service-contract.{ext}
        ├── {feature}.repository.{ext}
        └── tests/
            └── {feature}.service.spec.{ext}
```

## Adaptation Checklist / Lista de Adaptacion

**Checklist (EN):**
- [ ] Controllers do not contain business calculations, workflow branching, or persistence logic.
- [ ] Services accept DTOs or plain arguments instead of raw transport objects.
- [ ] Repositories and gateways are injected explicitly and coordinated from the service boundary.
- [ ] The main use case can be unit-tested without booting an HTTP server.
- [ ] Test coverage includes success, validation failure, and dependency-failure branches.
- [ ] Names, files, layers, and integrations were adapted to the target project's conventions instead of copying the example structure literally.

**Checklist (ES):**
- [ ] Los controladores no contienen calculos de negocio, ramas de flujo ni logica de persistencia.
- [ ] Los servicios reciben DTOs o argumentos planos en lugar de objetos crudos de transporte.
- [ ] Los repositorios y gateways se inyectan de forma explicita y se coordinan desde el limite del servicio.
- [ ] El caso de uso principal puede probarse sin levantar un servidor HTTP.
- [ ] La cobertura de pruebas incluye ramas de exito, fallo de validacion y fallo de dependencias.
- [ ] Los nombres, archivos, capas e integraciones se adaptaron a las convenciones del proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
