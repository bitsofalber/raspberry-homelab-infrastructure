# Raspberry Homelab Infrastructure

Self-hosted secure infrastructure running on Raspberry Pi using Docker, VPN isolation and automated backups.

## Overview

This project documents the design and deployment of a secure edge infrastructure environment including:

- Telegram community automation bot
- Self-hosted password manager (Vaultwarden)
- Automated encrypted off-site backups
- SSH hardening
- VPN-only service exposure (Tailscale)
- Containerized architecture (Docker)

The objective is to simulate a production-like environment on constrained hardware.

---

## Architecture

- Raspberry Pi (Debian-based)
- Dockerized services
- VPN access (Tailscale)
- SSH key-only authentication
- Automatic daily backups to external device
- Telegram alerting system

---

## Services Included

### Telegram Community Bot
Community automation and statistics collection.

### Vaultwarden (Self-hosted Bitwarden)
Private password manager accessible only via VPN.

### Backup Automation
Nightly encrypted backups with Telegram notifications.

---

## Security Measures

- No public port exposure
- VPN-only access
- SSH password authentication disabled
- Fail2Ban enabled
- Container isolation
- Capability dropping
- No new privileges

---

## Future Improvements

- Centralized monitoring
- Encrypted backup verification
- Reverse proxy with TLS
- Infrastructure as Code

---

Author: Alberto Hidalgo Moreno
