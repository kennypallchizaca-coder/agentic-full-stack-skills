---
name: 11-baas-integration
description: "Integrates BaaS providers through official SDKs, capability adapters, and secure client-server responsibility boundaries."
risk: high
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
BaaS platforms reduce backend work, but they also blur security boundaries if used carelessly. This skill standardizes official SDK setup, capability-based adapters, and the rule that privileged operations must stay behind security rules or server-side functions.

**Descripción (ES):**
Las plataformas BaaS reducen trabajo backend, pero también difuminan fronteras de seguridad si se usan sin cuidado. Esta skill estándariza el setup con SDK oficial, adaptadores por capacidad y la regla de que las operaciónes privilegiadas deben quedar detrás de reglas de seguridad o funciones server-side.

Related resources:
- [firebase-setup.template.md](./resources/firebase-setup.template.md)
- [baas-adapter-pattern.md](./resources/baas-adapter-pattern.md)

---

# 2. Skill Objective

**Objective (EN):**
Integrate Firebase or an equivalent BaaS safely without turning components into direct infrastructure code.
- Use this skill when: The app depends on an official BaaS SDK for auth, database, storage, or realtime features.
- Do not use this skill when: The frontend talks only to a custom backend and does not need a direct cloud SDK.

**Objetivo (ES):**
Integrar Firebase o un BaaS equivalente de forma segura sin convertir componentes en código de infraestructura.
- Úsese cuando: La app dependa de un SDK oficial BaaS para auth, base de datos, storage o realtime.
- No se use cuando: El frontend solo hable con un backend propio y no necesite SDK cloud directo.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Provider`: Firebase or an equivalent official SDK, such as Supabase, Appwrite, PocketBase, or a similar platform.
2. `Capability Map`: Which provider features the app really uses: auth, database, storage, realtime, functions, or edge logic.
3. `Public Config`: Public env variables required by the client SDK.
4. `Security Model`: Security rules, RLS, App Check, server functions, or edge functions.

**Entradas (ES):**
1. `Provider`: Firebase o un SDK oficial equivalente, como Supabase, Appwrite, PocketBase o una plataforma similar.
2. `Capability Map`: Que capacidades del provider usa realmente la app: auth, base de datos, storage, realtime, functions o edge logic.
3. `Public Config`: Variables publicas de entorno requeridas por el SDK cliente.
4. `Security Model`: Reglas de seguridad, RLS, App Check, server functions o edge functions.

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. A singleton provider bootstrap file.
2. Capability adapters or repositories consumed by the rest of the app.
3. Clear boundaries between client-safe operations and privileged server-side flows.
4. A documented handoff to session lifecycle handling and route protection.

**Salidas (ES):**
1. Un archivo singleton para inicializar el provider.
2. Adaptadores por capacidad o repositorios consumidos por el resto de la app.
3. Limites claros entre operaciónes seguras del cliente y flujos privilegiados del lado servidor.
4. Un handoff documentado hacia el manejo del ciclo de sesión y la protección de rutas.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Model provider capabilities first:** Decide whether the app uses auth, database, storage, realtime, or functions before exposing raw SDK calls to features.
2. **Bootstrap the SDK once:** Export a single initialized app or client instance from a shared module.
3. **Load only public client config:** Client-side API keys may be public by design, but admin keys and service secrets must stay server-side.
4. **Wrap SDK usage by capability:** Components should call app repositories, adapters, or services, not raw SDK primitives scattered everywhere.
5. **Keep auth lifecycle separate:** Session hydration, logout flow, and `401` recovery belong to Skill 06; provider setup and provider-specific hooks belong here.
6. **Keep route protection separate:** Router guards and navigation enforcement belong to Skill 12, even when auth state originates from the BaaS provider.
7. **Enforce backend-side protection:** Use rules, RLS, App Check, or server/edge functions for privileged operations.
8. **Document unsupported capabilities:** If the chosen provider does not own all features, state clearly which capabilities still depend on a custom backend.
9. **Adapt the pattern, not the literal example:** Rename files, provider adapters, session bridges, and server boundaries to match the chosen BaaS, framework, and project language.

**Instrucciones (ES):**
1. **Modela primero las capacidades del provider:** Decide si la app usa auth, base de datos, storage, realtime o functions antes de exponer llamadas crudas del SDK a los features.
2. **Inicializa el SDK una sola vez:** Exporta una única instancia inicializada del app o client desde un módulo compartido.
3. **Carga solo configuración publica:** Las client API keys pueden ser publicas por diseño, pero admin keys y secretos de servicio deben quedarse server-side.
4. **Envuelve el uso del SDK por capacidad:** Los componentes deben llamar repositorios, adaptadores o servicios de la app, no primitivas crudas del SDK por todas partes.
5. **Mantén separado el ciclo de auth:** La hidratación de sesión, el logout y la recuperación ante `401` pertenecen a la Skill 06; el setup del provider y sus hooks especificos viven aqui.
6. **Mantén separada la protección de rutas:** Los guards y la navegación protegida pertenecen a la Skill 12, incluso cuando el estado auth nace en el provider BaaS.
7. **Haz cumplir la protección del lado backend:** Usa rules, RLS, App Check o server/edge functions para operaciónes privilegiadas.
8. **Documenta capacidades no cubiertas:** Si el provider elegido no cubre todo, deja claro que partes siguen dependiendo de un backend propio.
9. **Adapta el patrón, no el ejemplo literal:** Renombra archivos, adaptadores del provider, puentes de sesión y límites server-side para ajustarlos al BaaS elegido, el framework y el lenguaje del proyecto.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @11-baas-integration to integrate `{BaaSProvider}` into this {Framework} app.
1. Create one shared SDK bootstrap and capability adapters for the provider features this app actually uses.
2. Keep privileged writes behind rules or server-side functions and hand off session lifecycle and route protection to the auth and guard layers.
```

**Prompt (ES):**
```text
Usa la skill @11-baas-integration para integrar `{BaaSProvider}` en esta app {Framework}.
1. Crea un bootstrap único del SDK y adaptadores por capacidad para las funciones del provider que la app realmente usa.
2. Mantén las escrituras privilegiadas detrás de rules o funciones server-side y delega el ciclo de sesión y la protección de rutas a las capas de auth y guards.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
├── shared/
│   └── baas/
│       ├── provider.client.{ext}
│       ├── adapters/
│       │   ├── auth.adapter.{ext}
│       │   ├── database.adapter.{ext}
│       │   └── storage.adapter.{ext}
│       └── session-bridge.{ext}
└── features/
    └── auth/
        └── store/
            └── auth.store.{ext}
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] The SDK is initialized exactly once.
- [ ] No service keys or admin credentials are exposed to the client bundle.
- [ ] Raw SDK primitives are hidden behind capability adapters or repositories.
- [ ] Security rules or server-side functions enforce privileged operations beyond UI checks.
- [ ] The boundary between provider setup, session lifecycle, and route protection is documented clearly.
- [ ] Names, files, provider adapters, session bridges, and server boundaries were adapted to the target project instead of copying the example structure literally.

**Checklist (ES):**
- [ ] El SDK se inicializa exactamente una vez.
- [ ] Ninguna service key ni credencial admin se expone al bundle del cliente.
- [ ] Las primitivas crudas del SDK quedan ocultas detrás de adaptadores por capacidad o repositorios.
- [ ] Las rules de seguridad o funciones server-side hacen cumplir operaciónes privilegiadas más allá de la UI.
- [ ] El límite entre setup del provider, ciclo de sesión y protección de rutas está documentado con claridad.
- [ ] Los nombres, archivos, adaptadores del provider, puentes de sesión y límites server-side se adaptaron al proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
