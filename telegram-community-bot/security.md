# Security Considerations

## Token Handling
The Telegram bot token is injected via environment variables.

## Data Persistence
Database stored in mounted Docker volume.

## Container Hardening
- no-new-privileges enabled
- All Linux capabilities dropped

## Exposure Model
Bot does not expose inbound ports.
Uses outbound API polling only.

## Limitations
SQLite not ideal for horizontal scaling.
Single-node design.
