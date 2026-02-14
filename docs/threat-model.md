# Threat Model

## Potential Threats

- Brute force SSH attacks
- Container breakout
- Credential theft
- Data loss
- Service exposure misconfiguration

---

## Mitigations

SSH brute force:
- Fail2Ban
- Key-only authentication

Credential exposure:
- Vaultwarden isolated behind VPN

Data loss:
- Automated daily off-site backups

Service exposure:
- No public ports
- VPN-only access

---

## Residual Risks

- Physical device compromise
- VPN account compromise
- Zero-day vulnerabilities
