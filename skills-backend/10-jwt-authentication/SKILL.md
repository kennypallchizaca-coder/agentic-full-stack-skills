---
name: 10-jwt-authentication
description: "Implements secure authentication with hashed passwords, minimal JWT claims and environment-managed secrets."
risk: high
universal: true
source: community
date_added: "2026-03-10"
---

# 1. Skill Description

**Description (EN):**
Authentication must protect credentials, issue trustworthy tokens, and keep secrets out of source code. A JWT (JSON Web Token) is a self-contained, digitally signed token composed of three parts — **header** (algorithm and type), **payload** (claims about the user), and **signature** (integrity proof) — transmitted as `header.payload.signature`. This skill defines a production-ready JWT flow with password hashing, minimal claims, secret management, token lifecycle, and clear validation boundaries. Token-based (stateless) authentication is the preferred method for REST APIs because it scales horizontally and works across domains, unlike session-based approaches which require server-side state.

**Descripción (ES):**
La autenticación debe proteger credenciales, emitir tokens confiables y mantener secretos fuera del código fuente. Un JWT (JSON Web Token) es un token autocontenido y firmado digitalmente compuesto por tres partes — **header** (algoritmo y tipo), **payload** (claims sobre el usuario) y **signature** (prueba de integridad) — transmitido como `header.payload.signature`. Esta skill define un flujo JWT listo para producción con hashing de contraseñas, claims mínimos, manejo de secretos, ciclo de vida del token y límites claros de validación. La autenticación basada en tokens (stateless) es el método preferido para APIs REST porque escala horizontalmente y funciona entre dominios, a diferencia de enfoques basados en sesión que requieren estado en el servidor.

Related resources:
- [jwt-claims.schema.json](./resources/jwt-claims.schema.json)

---

# 2. Skill Objective

**Objective (EN):**
Build a secure login flow that issues and validates JWTs without leaking secrets or overloading the token payload, adapting to the chosen auth architecture.
- Use this skill when: Implementing email/password login, token validation middleware, or refresh/access token flows.
- Do not use this skill when: Authentication is fully delegated to an external identity provider with no local token issuance.

**Objetivo (ES):**
Construir un flujo de login seguro que emita y valide JWTs sin filtrar secretos ni sobrecargar el payload, adaptándolo a la arquitectura de autenticación elegida.
- Úsese cuando: Se implemente login por email/password, middleware de validación de tokens o flujos refresh/access token.
- No se use cuando: La autenticación esté delegada por completo a un proveedor externo sin emisión local de tokens.

---

# 3. Inputs / Entradas

**Inputs (EN):**
1. `Credential Source`: User email/username plus password hash stored in the database.
2. `Token Claims`: Minimal identity and authorization data. Standard claims include `sub` (subject/user ID), `iat` (issued at), `exp` (expiration), `iss` (issuer), `aud` (audience), and custom claims like `roles`. Never include passwords, sensitive profile data, or large objects in the payload.
3. `Secret Strategy`: Environment variables, secret manager, or asymmetric keys (RS256 for distributed systems, HS256 for single-service).

**Entradas (ES):**
1. `Credential Source`: Email/usuario más hash de contraseña almacenado en base de datos.
2. `Token Claims`: Datos mínimos de identidad y autorización. Los claims estándar incluyen `sub` (sujeto/ID de usuario), `iat` (emisión), `exp` (expiración), `iss` (emisor), `aud` (audiencia) y claims personalizados como `roles`. Nunca incluyas passwords, datos sensibles del perfil ni objetos grandes en el payload.
3. `Secret Strategy`: Variables de entorno, secret manager o llaves asimétricas (RS256 para sistemas distribuidos, HS256 para servicio único).

---

# 4. Outputs / Salidas

**Outputs (EN):**
1. Password hashing and verification routines using adaptive algorithms (bcrypt, argon2).
2. Token issuing and token verification services or middleware.
3. A safe login response contract that returns the token and basic user info but **never** the password, hash, or secret keys.
4. Secret-loading configuration isolated from application code.

**Salidas (ES):**
1. Rutinas de hashing y verificación de contraseñas usando algoritmos adaptativos (bcrypt, argon2).
2. Servicios o middleware para emitir y validar tokens.
3. Un contrato seguro de respuesta de login que devuelva el token e info básica del usuario pero **nunca** el password, hash ni claves secretas.
4. Configuración de carga de secretos aislada del código de aplicación.

---

# 5. Execution Steps

**Instructions (EN):**
1. **Hash passwords securely:** Use `bcrypt`, `argon2`, or an equivalent adaptive algorithm. Never store plaintext passwords. Enforce minimum password policies (length, complexity) at the validation layer.
2. **Issue minimal claims:** Put only what the backend must trust in the token (`sub`, roles, expiry, issuer/audience when relevant). The JWT payload is encoded but **not encrypted** — anyone can decode it, so never embed passwords, emails, or sensitive profile data.
3. **Load secrets from secure config:** Read signing secrets or keys from environment variables or a secret manager. Never hardcode them. Use strong, random secrets — weak secrets compromise every token in the system.
4. **Validate every token use:** Check signature, expiration, issuer/audience as needed, and reject malformed or expired tokens deterministically. Return `401 Unauthorized` for absent, invalid, or expired tokens.
5. **Implement access + refresh token lifecycle:** Issue short-lived access tokens (15–60 minutes) for API requests and longer-lived refresh tokens (days) for session renewal. Rotate refresh tokens on each use. Store refresh tokens securely — never in `localStorage` for web clients.
6. **Guard against common pitfalls:** Avoid tokens that never expire, secrets committed to the repository, credentials transmitted over HTTP (require HTTPS), and tokens logged or exposed in URLs. Implement brute-force protection on login endpoints.
7. **Adapt the pattern, not the literal example:** Rename files, layers, contracts, and integrations to match the target project's architecture, framework conventions, and business language.

**Instrucciones (ES):**
1. **Hashear contraseñas de forma segura:** Usa `bcrypt`, `argon2` o un algoritmo adaptativo equivalente. Nunca guardes passwords en texto plano. Aplica políticas mínimas de contraseña (longitud, complejidad) en la capa de validación.
2. **Emitir claims mínimos:** Pon solo lo que el backend debe confiar dentro del token (`sub`, roles, expiración, issuer/audience si aplica). El payload JWT está codificado pero **no encriptado** — cualquiera puede decodificarlo, así que nunca incluyas passwords, emails ni datos sensibles del perfil.
3. **Cargar secretos desde configuración segura:** Lee secretos o llaves desde variables de entorno o un secret manager. Nunca los hardcodees. Usa secretos fuertes y aleatorios — secretos débiles comprometen todos los tokens del sistema.
4. **Validar cada uso del token:** Revisa firma, expiración, issuer/audience cuando aplique y rechaza tokens malformados o vencidos de forma determinista. Devuelve `401 Unauthorized` para tokens ausentes, inválidos o expirados.
5. **Implementar ciclo access + refresh token:** Emite access tokens de vida corta (15–60 minutos) para requests a la API y refresh tokens de vida más larga (días) para renovación de sesión. Rota los refresh tokens en cada uso. Almacénalos de forma segura — nunca en `localStorage` para clientes web.
6. **Prevenir errores comunes:** Evita tokens sin expiración, secretos commiteados al repositorio, credenciales transmitidas por HTTP (exige HTTPS) y tokens logueados o expuestos en URLs. Implementa protección contra fuerza bruta en endpoints de login.
7. **Adapta el patrón, no el ejemplo literal:** Renombra archivos, capas, contratos e integraciones para ajustarlos a la arquitectura, las convenciones del framework y el lenguaje de negocio del proyecto objetivo.

---

# 6. Example Usage (Prompt)

**Prompt (EN):**
```text
Use the skill @10-jwt-authentication to implement secure login for `{AuthModule}`.
1. Hash passwords with an adaptive algorithm and issue JWTs with minimal claims (sub, roles, exp).
2. Load signing secrets from environment configuration, validate token expiry on every protected request, and implement refresh token rotation.
```

**Prompt (ES):**
```text
Usa la skill @10-jwt-authentication para implementar login seguro en `{AuthModule}`.
1. Hashea contraseñas con un algoritmo adaptativo y emite JWTs con claims mínimos (sub, roles, exp).
2. Carga los secretos de firma desde configuración de entorno, valida la expiración en cada request protegida e implementa rotación de refresh tokens.
```

---

# 7. Recommended File Structure / Estructura Recomendada

```text
src/
├── core/
│   └── auth/
│       ├── auth-config.{ext}
│       ├── token-service.{ext}
│       └── request-auth.{ext}
└── modules/
    └── auth/
        ├── dto/
        │   ├── login.dto.{ext}
        │   └── register.dto.{ext}
        ├── auth-service.{ext}
        └── auth.controller.{ext}
```

## Adaptation Checklist / Lista de Adaptación

**Checklist (EN):**
- [ ] Passwords are stored only as secure hashes, never in plaintext.
- [ ] JWT secrets or private keys are not committed to the repository.
- [ ] Protected routes reject expired, malformed, or tampered tokens with `401`.
- [ ] The login response never includes passwords, hashes, or internal secrets.
- [ ] The JWT payload does not contain sensitive or unnecessarily large data.
- [ ] Refresh tokens rotate on each use and are stored securely.
- [ ] Names, files, layers, and integrations were adapted to the target project's conventions instead of copying the example structure literally.

**Checklist (ES):**
- [ ] Las contraseñas se almacenan solo como hashes seguros, nunca en texto plano.
- [ ] Los secretos JWT o llaves privadas no se suben al repositorio.
- [ ] Las rutas protegidas rechazan tokens expirados, malformados o alterados con `401`.
- [ ] La respuesta de login nunca incluye passwords, hashes ni secretos internos.
- [ ] El payload JWT no contiene datos sensibles ni innecesariamente grandes.
- [ ] Los refresh tokens rotan en cada uso y se almacenan de forma segura.
- [ ] Los nombres, archivos, capas e integraciones se adaptaron a las convenciones del proyecto objetivo en lugar de copiar literalmente la estructura de ejemplo.
