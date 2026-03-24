# Edge and Runtime Matrix

Use this matrix to match deployment shape to the actual runtime instead of forcing every project into the same ops stack.

| Target | Best fit | Strengths | Watch-outs |
|---|---|---|---|
| Container host | Docker image + service manifest | Portable, reproducible, common in teams | Need image hygiene, health checks, and image scanning |
| PaaS | Buildpack or container deploy | Fast setup, simple rollback, managed networking | Platform-specific env and health conventions |
| VM or bare server | Native process + supervisor | Useful for legacy or cost-sensitive setups | More manual patching, TLS, and process management |
| Serverless | Function packaging + env-based config | Scales on demand, low idle cost | Cold starts, request limits, stateless constraints |
| Edge runtime | Lightweight handler bundle | Very low latency near users | Restricted runtime APIs, limited drivers, short execution windows |

## Selection rule

- Prefer the simplest runtime that still satisfies security, observability, scaling, and rollback needs.
- Do not force containers if the platform already gives reliable native deployment primitives.
- Do not force serverless or edge when the app depends on long-lived connections, heavy binaries, or local filesystem state.
