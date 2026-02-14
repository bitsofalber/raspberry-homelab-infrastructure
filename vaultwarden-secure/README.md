# Vaultwarden Secure Deployment (Raspberry Pi)

Self-hosted Bitwarden-compatible password manager deployed securely on Raspberry Pi using Docker and VPN-only access.

---

## Objective

Deploy a production-style password manager with:

- Zero public exposure
- VPN-only access (Tailscale)
- Container hardening
- 2FA enforcement
- Automated off-site encrypted backups
- Telegram alerting integration

---

## Architecture

Client Device  
→ Tailscale VPN  
→ Raspberry Pi  
→ Docker container (Vaultwarden)  
→ SQLite database (persistent volume)

Service bound to localhost and exposed securely through Tailscale HTTPS serve.

---

## Deployment

```bash
cd docker
docker compose up -d

-- 

Accedes mediante: https://hostname.tailnet.ts.net

--

Security Controls
	•	No public ports exposed
	•	Localhost binding (127.0.0.1)
	•	VPN-only access
	•	Signups disabled
	•	Admin token required
	•	Container capability dropping
	•	no-new-privileges enabled
	•	SSH key-only authentication
	•	Fail2Ban active



Backup Strategy
	•	Nightly automated tar backup
	•	Secure transfer via SCP to external device
	•	Telegram success/failure notification
	•	Local retention cleanup policy



Threat Model

Attack Surface
	•	VPN compromise
	•	Stolen trusted device
	•	Backup failure
	•	Container escape



Mitigation
	•	Tailscale private mesh
	•	2FA enabled
	•	Off-device backups
	•	Strict SSH configuration
	•	Minimal container privileges



Future Improvements
	•	GPG encrypted backups
	•	Backup integrity hash verification
	•	Reverse proxy with TLS termination
	•	Infrastructure as Code
	•	Secret management refinement


Author: Alberto Hidalgo Moreno
Focus: Cybersecurity | DevSecOps | Infrastructure Hardening
