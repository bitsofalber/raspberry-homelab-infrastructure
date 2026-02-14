# Architecture Design

## Design Goals

- Lightweight
- Self-hosted
- Low resource usage (Raspberry Pi compatible)
- Persistent data
- No third-party SaaS dependency

---

## Components

### Telegram API
Handles inbound and outbound messages via long polling.

### Application Layer
Python-based bot using python-telegram-bot.

### Persistence Layer
SQLite database for:
- Message statistics
- Activity tracking
- Milestone state memory

### Scheduler
JobQueue handles:
- Member milestone checks
- Scheduled notifications
