# Reverse Proxy Template

Use this template when a backend sits behind Nginx, Caddy, Traefik, an ingress controller, or another HTTP edge layer.

## Edge responsibilities

- Terminate TLS or trust a platform-managed TLS layer.
- Forward the original host, client IP, and protocol headers the app needs.
- Route API traffic to the backend service port.
- Expose health or readiness endpoints for platform checks when required.
- Apply rate limiting, request-size limits, and timeout rules appropriate to the API.

## Minimum checklist

- Preserve `X-Forwarded-For`, `X-Forwarded-Proto`, and host information if the app depends on them.
- Keep upstream timeouts aligned with long-running but valid requests.
- Do not expose admin dashboards or internal ports publicly by default.
- Return consistent error pages or pass backend error envelopes through intentionally.
- Document whether security headers are set at the proxy, the app, or both.

## Platform examples

- Nginx site or server block
- Caddy site definition
- Traefik dynamic config
- Kubernetes ingress or gateway manifest

## Adaptation rule

Use the platform's native syntax, but keep the same decisions explicit: TLS, forwarded headers, health routing, timeouts, and abuse protections.
