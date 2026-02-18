# 🤖 Telegram Community Bot: Infrastructure & Automation

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Raspberry Pi](https://img.shields.io/badge/Hardware-Raspberry_Pi-C51A4A?style=for-the-badge&logo=raspberry-pi&logoColor=white)
![Security](https://img.shields.io/badge/Security-VPN_Only-000000?style=for-the-badge&logo=tailscale&logoColor=white)

Este proyecto forma parte de mi **Raspberry Homelab Infrastructure**. Se trata de un bot de automatización diseñado bajo un enfoque de despliegue en producción, priorizando la seguridad, la persistencia de datos y el control de infraestructura en entornos de hardware limitado.

---

## 🎯 Objetivo del Proyecto

Desplegar un servicio modular de gestión de comunidades con capacidades de orquestación de hardware local, implementando:
* **Persistencia:** Base de datos SQLite integrada en volúmenes Docker.
* **Automatización:** Programación de tareas en segundo plano (JobQueue).
* **Control de Infraestructura:** Integración de comandos Wake-on-LAN (WOL).
* **Seguridad:** Modelo de privilegios mínimos y acceso restringido vía VPN.

---

## 💻 Stack Tecnológico

| Componente | Tecnología |
| :--- | :--- |
| **Lenguaje** | `Python 3.11` (Asyncio) |
| **Framework** | `python-telegram-bot` |
| **Base de Datos** | `SQLite` |
| **Despliegue** | `Docker` & `Docker Compose` |
| **Red / Seguridad** | `Tailscale` (VPN) |
| **Hardware** | `Raspberry Pi` (ARM-based) |

---

## ⚡ Funcionalidades Destacadas

### 👥 Gestión de Comunidad y Analytics
* **Moderación Inteligente:** Mensajes de bienvenida temporales (auto-borrado 24h) y sistema de advertencias.
* **Comandos de Consulta:** `/whoami` (lookup de usuario) y `/rules` dinámicas.
* **Estadísticas:** Tracking de actividad y rankings de usuarios activos (`/top`).
* **Notificaciones:** Anuncios programados ante hitos de la comunidad.

### 🖥️ Remote Power Control (WOL)
Integración de bajo nivel para la gestión de energía de equipos en la LAN local:
* **`/pc`**: Envío de paquetes mágicos (Wake-on-LAN) desde el contenedor.
* **`/pc_status`**: Verificación de estado mediante ICMP ping.
* **Restricción:** Acceso exclusivo para el `ADMIN_ID`.

---

## 🏗️ Arquitectura y Seguridad

### Modelo de Despliegue
```text
Telegram API ↔️ Docker Container (Non-root) ↔️ SQLite (Persistent Volume)
                                   ↳ JobQueue (Async Tasks)
                                   ↳ LAN Broadcast (WOL)
```

Endurecimiento (Hardening) de Seguridad
User Namespace: Ejecución del contenedor con usuario no privilegiado.

Capabilities: Eliminación de capacidades del kernel (cap_drop).
Privilegios: no-new-privileges habilitado en el runtime de Docker.
Aislamiento: Sin exposición de puertos públicos; acceso total gestionado por túneles VPN.
Secrets: Gestión estricta de variables de entorno mediante archivos .env (fuera del repositorio).

## 🚀 Despliegue Rápido
1. Preparar Entorno
Crea un archivo .env en la raíz del proyecto:

```bash
BOT_TOKEN=tu_token_aqui
ADMIN_CHAT_ID=tu_id_aqui
```
**Ejecución**

```bash
docker logs -f telegram-community-bot
```
## 🎓 Resultados de Aprendizaje

Este proyecto demuestra competencias en:

Despliegue de aplicaciones Python containerizadas.
Gestión de persistencia de datos en Docker.
Orquestación de tareas asíncronas.
DevOps Mindset: Documentación técnica clara y orientada a la seguridad.


[⬅️ Volver al inicio](../README.md)


