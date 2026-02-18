# 🔐 Vaultwarden Secure Deployment

![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Security](https://img.shields.io/badge/Security-Hardened-red?style=for-the-badge&logo=guardant&logoColor=white)
![VPN](https://img.shields.io/badge/Access-VPN_Only-000000?style=for-the-badge&logo=tailscale&logoColor=white)
![Platform](https://img.shields.io/badge/Hardware-Raspberry_Pi-C51A4A?style=for-the-badge&logo=raspberry-pi&logoColor=white)

Despliegue de un gestor de contraseñas compatible con Bitwarden (Vaultwarden) en una infraestructura **Raspberry Pi**, bajo un modelo de **Zero Public Exposure**. Este proyecto se enfoca en la máxima privacidad y el endurecimiento de contenedores.

---

## 🎯 Objetivos del Despliegue
* **Privacidad Total:** Acceso exclusivo mediante **Tailscale VPN**.
* **Seguridad Ofensiva:** Implementación de políticas contra el escalado de privilegios.
* **Resiliencia:** Backups automatizados y cifrados fuera del sitio (Off-site).
* **Monitorización:** Integración con Telegram para alertas de estado y backups.

---

## 🏗️ Arquitectura del Sistema
El flujo de conexión garantiza que el servicio nunca sea visible desde el internet público:

```text
Dispositivo Cliente 🛡️ ↔️ Tailscale VPN ↔️ Raspberry Pi (Localhost)
                                        ↳ Docker (Vaultwarden)
                                        ↳ SQLite (Volumen Persistente)
```

Nota técnica: El servicio está bindeado a 127.0.0.1 y expuesto de forma segura mediante Tailscale HTTPS.

## 🔒 Controles de Seguridad (Hardening)

| Área        | Medidas aplicadas |
|------------|------------------|
| **Red**    | Zero Public Ports, Localhost binding, Fail2Ban activo |
| **Acceso** | VPN-only, SSH Key-only, Registro de nuevos usuarios deshabilitado |
| **Contenedor** | `cap_drop` (todas), `no-new-privileges` habilitado |
| **Gestión** | Admin Token requerido, Enforce 2FA |

🚀 Despliegue y Mantenimiento

Levantamiento del Stack

```bash
cd docker
docker compose up -d
```
Acceso mediante: https://hostname.tailnet.ts.net

## Estrategia de Backup

Frecuencia: Copia de seguridad automatizada cada noche (Tar).
Transferencia: Envío seguro vía SCP a dispositivo externo.
Alerting: Notificación instantánea de éxito/error vía Telegram.
Limpieza: Política automática de retención de copias antiguas.

## 📈 Roadmap de Mejoras (Future Work)

[ ] Cifrado de backups mediante GPG.
[ ] Verificación de integridad de backups (Hash verification).
[ ] Implementación de Infraestructura como Código (IaC).
[ ] Refinamiento en la gestión dinámica de secretos.

[⬅️ Volver al proyecto](./README.md)

