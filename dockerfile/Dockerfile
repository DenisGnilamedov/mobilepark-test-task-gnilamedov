FROM python:3.12-slim as builder
COPY requirements.txt /requirements.txt

RUN apt-get update && apt-get install -y --no-install-recommends \
    python3-dev build-essential \
    && rm -rf /var/lib/apt/lists/*

RUN python3 -m venv /venv   \
    && source /venv/bin/activate \
    && pip install --no-cache-dir -r /requirements.txt

FROM python:3.12-slim
WORKDIR /app

# Уменьшают мусор
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PATH="/venv/bin:$PATH"

# Добавляем юзера, от имени которого будет выполняться код для безопасности
RUN useradd -m python-user
USER python-user

COPY --from=builder /venv /venv

COPY --chown=python-user:python-user app.py /app/app.py
EXPOSE 5000
CMD ["python", "app.py"]

