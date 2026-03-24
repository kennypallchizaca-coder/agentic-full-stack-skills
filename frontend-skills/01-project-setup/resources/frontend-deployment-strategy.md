# Frontend Deployment Strategy

Use this guide to choose a hosting strategy before turning deployment into automation.

## Delivery targets

| Target | Best fit | Key requirement |
|--------|----------|-----------------|
| Static site | Docs, blogs, marketing pages, Astro static output | Build produces self-contained assets |
| SPA hosting | Client-rendered apps with router fallback | Host must redirect unknown routes to `index.html` or equivalent |
| Hybrid / SSR | Apps with server rendering or server actions | Hosting must support runtime execution, not just static assets |

## Questions to answer first

- Is the app fully static, SPA-only, or hybrid/server-rendered?
- Does the router require fallback behavior for deep links?
- Does the app need a custom base path such as `/my-app/`?
- Which environment variables are public and which belong only to the server/runtime?

## Hosting notes

- **GitHub Pages:** Works well for static output and some SPAs if base path and route fallback are handled carefully.
- **Netlify / Cloudflare Pages:** Good for static and SPA hosting, with optional functions depending on the platform.
- **Vercel / Render / Railway:** Better fit for hybrid and server-rendered frontends.
