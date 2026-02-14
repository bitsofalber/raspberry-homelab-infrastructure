FROM python:3.11-slim

# =========================
# Variables internas
# =========================
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# =========================
# Crear usuario no root
# =========================
RUN addgroup --system appgroup && \
    adduser --system --ingroup appgroup appuser

# =========================
# Crear directorio app
# =========================
WORKDIR /app

# =========================
# Instalar dependencias mínimas
# =========================
RUN apt-get update && apt-get install -y \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# =========================
# Copiar requirements
# =========================
COPY src/requirements.txt ./requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# =========================
# Copiar código
# =========================
COPY src/ ./src/

# =========================
# Crear directorio datos con permisos correctos
# =========================
RUN mkdir -p /app/data && \
    chown -R appuser:appgroup /app

# =========================
# Cambiar a usuario no root
# =========================
USER appuser

# =========================
# Ejecutar bot
# =========================
CMD ["python", "src/bot.py"]
