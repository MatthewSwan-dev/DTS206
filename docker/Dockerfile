# ── Stage 1: Builder ─────────────────────────────────
# Full Python image — needed to compile dependencies
FROM python:3.11 AS builder
WORKDIR /build
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# ── Stage 2: Production ───────────────────────────────
# Slim image — no build tools, no pip, no gcc
FROM python:3.11-slim

# Non-root user BEFORE copying anything
RUN groupadd -r appgroup && \
    useradd -r -g appgroup -u 1001 -m appuser

WORKDIR /app

# Copy ONLY compiled packages from builder — not pip itself
COPY --from=builder /usr/local/lib/python3.11 /usr/local/lib/python3.11
COPY --from=builder /usr/local/bin/python /usr/local/bin/python
COPY app.py .

# Set ownership BEFORE switching user
RUN chown -R appuser:appgroup /app

# Switch to non-root — everything after this runs as appuser
USER appuser

HEALTHCHECK --interval=30s --timeout=10s --retries=3 \
  CMD python -c "import urllib.request; urllib.request.urlopen('http://localhost:8080/health')"

EXPOSE 8080
CMD ["python", "app.py"]