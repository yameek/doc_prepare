# Packaging & Deployment in FastAPI

## 1. Uvicorn (ASGI Server)
Use `gunicorn` with `uvicorn` workers for production resilience.

`pip install "uvicorn[standard]" gunicorn`

Run:
`gunicorn main:app --workers 4 --worker-class uvicorn.workers.UvicornWorker --bind 0.0.0.0:8000`

## 2. Dockerfile
Multistage builds are great for keeping images small.

```dockerfile
# Build stage
FROM python:3.11 as requirements-stage
WORKDIR /tmp
RUN pip install poetry
COPY ./pyproject.toml ./poetry.lock* /tmp/
RUN poetry export -f requirements.txt --output requirements.txt --without-hashes

# Run stage
FROM python:3.11-slim
WORKDIR /code
COPY --from=requirements-stage /tmp/requirements.txt /code/requirements.txt
RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt
COPY ./app /code/app

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "80"]
```

## 3. HTTPS
Terminate SSL at a reverse proxy (Nginx, Traefik, ALB) and talk HTTP to the container.
