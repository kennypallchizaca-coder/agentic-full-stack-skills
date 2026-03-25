# Environment Exposure (Variables de Entorno Client-Side)

En frontend, cualquier valor expuesto al bundle puede terminar en el navegador del usuario. Por eso cada framework define una barrera entre variables publicas y privadas. Usa siempre el mecanismo oficial del stack en lugar de asumir que cualquier clave del `.env` es segura para cliente.

## Vite (React, Vue)

- Public exposure prefix: `VITE_`
- Access pattern: `import.meta.env.VITE_API_URL`

```env
VITE_API_URL=https://api.example.com
VITE_STRIPE_PUBLIC_KEY=pk_test_123

# Server-only values remain private:
DB_PASSWORD=server-only-value
```

---

## Astro

- Public exposure prefix: `PUBLIC_`
- Access pattern: `import.meta.env.PUBLIC_API_URL`

```env
PUBLIC_API_URL=https://api.example.com

# Astro also runs in server/edge contexts; values without `PUBLIC_` stay server-side.
SECRET_API_KEY=server-only-value
```

---

## Create React App (legacy)

- Legacy public prefix: `REACT_APP_`
- Access pattern: `process.env.REACT_APP_API_URL`

```env
REACT_APP_API_URL=https://api.example.com
```

---

## Angular (native environments)

Angular usually does not depend on `.env` prefixes by default; it commonly swaps Typescript config files at build time through file replacements. If a project adds `.env` support, it must define explicitly which variables are safe to expose to the browser.

Common Angular pattern:
Filename: `src/environments/environment.ts`
```typescript
export const environment = {
  production: false,
  apiUrl: 'https://api.example.com'
};
```

## Universal Rule

- Treat every browser-exposed variable as public information.
- Keep database credentials, private API keys, signing secrets, and service-account credentials outside the frontend runtime.
- If the framework offers both public and private env scopes, document the boundary in the project README or setup checklist.
