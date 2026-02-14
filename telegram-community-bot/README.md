# Telegram Community Bot

Automated moderation and engagement bot designed for managing and scaling Telegram communities.

## Overview

This project implements a self-hosted Telegram bot deployed via Docker on a Raspberry Pi.  
It provides moderation tools, community analytics, milestone announcements, and infrastructure monitoring alerts.

---

## Features

### Community Management
- Automated welcome messages (auto-delete after 24h)
- Rules command
- User info lookup
- Warning system
- Admin announcements with optional pin

### Engagement & Analytics
- Member milestone auto-announcements
- Activity tracking (SQLite-based)
- Top active users command
- Scheduled background jobs

### Infrastructure Integration
- Telegram-based system alerts
- Backup status notifications
- Container-based deployment

---

## Architecture

Telegram API  
↓  
Docker container  
↓  
SQLite database  
↓  
Scheduled Jobs (JobQueue)

---

## Deployment

```bash
docker compose up -d --build
