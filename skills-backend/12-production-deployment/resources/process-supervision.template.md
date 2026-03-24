# Process Supervision Template

Use this template when the backend runs as a native process instead of inside a long-lived container platform.

## Required supervision behaviors

- Start automatically after reboot or host restart.
- Restart on crash with a bounded backoff policy.
- Write stdout/stderr to the platform's log collector or a managed log file.
- Load env vars from a secure location instead of hardcoded inline secrets.
- Stop gracefully on termination signals so in-flight work can finish safely.

## Runtime checklist

- Define the exact start command for the release artifact.
- Confirm the working directory and writable paths are explicit.
- Expose the HTTP port through config rather than hardcoding it.
- Keep migrations and smoke checks as separate release steps, not process start side effects.

## Platform examples

- `systemd` service on Linux
- PM2 or another process manager for Node.js
- Windows service wrapper
- Supervisor or equivalent host-native daemon manager
