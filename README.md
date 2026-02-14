# Raspberry Homelab Infrastructure

Self-hosted secure infrastructure running on Raspberry Pi using Docker, VPN isolation, container hardening and automated off-site backups.

---

## Overview

This repository documents the design, deployment and security hardening of a production-like edge infrastructure running on constrained hardware (Raspberry Pi).

The objective is to simulate real-world secure service deployment with:

- Zero public attack surface
- VPN-only exposure model
- Container isolation and least privilege
- Automated off-site backups
- Real-time alerting
- Operational security controls

This project serves as a practical DevSecOps / Blue Team lab environment.

---

## High-Level Architecture

### Core Stack

- Raspberry Pi (Debian-based)
- Docker containerization
- Tailscale (WireGuard-based VPN mesh)
- SSH key-only authentication
- Automated backup pipeline
- Telegram alerting integration

### Security Model

User Device  
→ Tailscale VPN  
→ Raspberry Pi  
→ Dockerized services (isolated)

No services are exposed to the public internet.

---

## Components

###  Telegram Community Bot

Dockerized Telegram bot designed for:

- Community automation
- User statistics tracking
- Activity monitoring
- Scheduled jobs
- Alerting integrations

**Key characteristics:**

- SQLite-based message tracking
- Persistent Docker volume storage
- Background job scheduling
- Command-based modular handlers

**Security controls:**

- No direct public exposure
- Token isolation via environment variables
- Container capability dropping
- `no-new-privileges` enabled

---

###  Vaultwarden (Self-hosted Password Manager)

Lightweight Bitwarden-compatible password manager deployed in Docker.

**Access model:**

- Bound to localhost
- Exposed only via Tailscale HTTPS serve
- 2FA enabled (TOTP)
- Signups disabled
- Admin token protected

**Architecture:**

Browser Client  
→ Tailscale HTTPS endpoint  
→ Vaultwarden container  
→ SQLite database (persistent volume)

**Security posture:**

- No public ports exposed
- VPN-only access
- Master password locally derived
- Daily off-site backups
- Container privilege restrictions

---

### Automated Off-Site Backup System

Custom Bash-based backup pipeline.

**Process:**

1. Archive Vaultwarden data directory  
2. Generate timestamped compressed backup  
3. Securely transfer to external machine (Mac)  
4. Send Telegram success/failure notification  
5. Local retention cleanup policy  

**Security properties:**

- No cloud storage dependency
- Encrypted transport (SSH)
- Off-device redundancy
- Failure alerting
- Backup integrity validation via test extraction

---

## Security Hardening

Infrastructure-level protections implemented:

- SSH password authentication disabled
- Key-only SSH access
- Fail2Ban enabled
- No open inbound public ports
- Tailscale private mesh network
- Container capability dropping
- `no-new-privileges` enabled
- Localhost binding for internal services
- Principle of least privilege applied

Attack surface intentionally minimized.

---

## Threat Model Summary

### Primary Risks Considered

- Internet-facing exposure
- Credential brute-force attempts
- Container breakout
- Data loss
- Backup failure
- Lateral movement via SSH

### Mitigations Implemented

- VPN-only exposure model
- Strict SSH configuration
- No public service binding
- Off-site backups
- Real-time Telegram alerts
- Docker isolation controls

Residual risk is limited to compromised trusted device or VPN account breach.

---

## Operational Model

Daily Operations:

- Telegram bot active and persistent
- Vaultwarden accessible via Tailscale HTTPS
- Nightly automated backups
- Alert notifications for backup success/failure

Infrastructure can be fully restarted via Docker with persistent volumes preserved.

---

## Future Improvements

- Centralized logging (Prometheus / Grafana / Loki)
- Intrusion detection experimentation
- Infrastructure as Code (Ansible/Terraform)
- Backup encryption with GPG
- CI/CD validation pipeline
- Secrets management refinement

---

## Purpose

This project is designed to:

- Demonstrate secure service deployment on edge hardware
- Apply real-world hardening techniques
- Practice DevSecOps fundamentals
- Build operational security discipline
- Serve as a personal infrastructure laboratory

---

**Author:** Alberto Hidalgo Moreno  
**Focus:** Cybersecurity | DevSecOps | Infrastructure Hardening | ASIR students
