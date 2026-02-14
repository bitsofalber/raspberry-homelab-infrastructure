---

```markdown
## Detailed Architecture

Vaultwarden runs inside a Docker container with:

- SQLite database persistence
- RSA key generation
- WebSocket support enabled
- Localhost binding for zero exposure

HTTPS is provided via Tailscale Serve.

Data flow:

Browser → Tailscale HTTPS → Localhost → Docker → SQLite
