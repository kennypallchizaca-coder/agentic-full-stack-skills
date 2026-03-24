# Frontend Delivery Checklist

Use this checklist when the project setup must leave a reliable delivery baseline instead of only a compilable project.

## Universal baseline

- `lint`: static analysis or framework-equivalent quality check
- `typecheck`: TypeScript, template type check, or framework compiler validation
- `build`: production build command
- `preview` or `start:prod`: a way to verify the production artifact locally
- `.env.example`: only client-safe variables documented

## Stack notes

### Vite-style apps

- Alias mirrored in `tsconfig` and bundler config
- Public env variables use the stack's explicit public prefix
- `npm run build` or equivalent is part of the normal pre-ship flow

### Angular

- Keep `build`, template checks, and environment files explicit
- Prefer a documented production build command over manual one-off CLI usage
- If the project is deployed statically, confirm `baseHref` and `deployUrl` behavior before shipping

### Astro

- Decide early whether the project is static-first, server, or hybrid
- Keep formatter/linter tooling explicit because content-heavy repos drift quickly
- If static deployment is expected, document the target and output directory clearly

## Pre-publish checklist

- [ ] A new contributor can find the quality commands without reading source code
- [ ] Env exposure rules are documented and safe
- [ ] Build output can be reproduced locally
- [ ] The deployment target is named, even if the final pipeline is not implemented yet
- [ ] The project does not depend on hidden machine-local config
