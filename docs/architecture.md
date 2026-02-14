# Infrastructure Architecture

## Network Design

All services are isolated inside Docker containers.
No service is exposed directly to the internet.

Access model:

Client Device
    ↓
Tailscale VPN
    ↓
Raspberry Pi
    ↓
Docker Services

---

## Service Exposure Policy

Vaultwarden:
- Bound to 127.0.0.1
- Exposed via Tailscale Serve (HTTPS)

Telegram Bot:
- Outbound-only API communication

Backups:
- Secure SCP transfer via SSH keys

---

## Security Layers

1. SSH key-based authentication only
2. Password authentication disabled
3. Fail2Ban active
4. No direct WAN exposure
5. VPN-based segmentation
