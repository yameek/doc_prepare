# Docker & Microservices Guide

## 🐳 Dockerize Your Application

### 1. The `Dockerfile`
Create a `Dockerfile` in your project root.

**FastAPI Example:**
```dockerfile
# Base image
FROM python:3.10-slim

# Set working directory
WORKDIR /app

# Install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy project code
COPY . .

# Expose port
EXPOSE 8000

# Command to run (using shell form to allow variable expansion if needed, or exec form preferably)
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

**Django Example:**
```dockerfile
FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000

# Often you might use a shell script (entrypoint.sh) to run migrations before starting
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
```

### 2. `.dockerignore`
ALWAYS create a `.dockerignore` file to prevent copying unnecessary files (keeps image small and secure).
```text
__pycache__
*.pyc
.git
.env
venv/
```

## 🕸️ Microservices Approach

In a microservices architecture, you split your application into smaller, independent services (e.g., Auth Service, Product Service) and use a "Middleware" (Reverse Proxy/API Gateway) to route requests. You also often need a shared state or message broker like Redis.

### Flow Setup
Client -> **Reverse Proxy (Nginx/Traefik)** -> **Service A / Service B**
Services <-> **Redis (Cache/Queue)**
Services <-> **Database**

### `docker-compose.yml`
This wraps everything together for local development.

```yaml
version: '3.8'

services:
  # --- Service 1: FastAPI Web App ---
  web:
    build: .
    command: uvicorn main:app --host 0.0.0.0 --port 8000
    volumes:
      - .:/app  # Live reload for development
    ports:
      - "8000:8000"
    depends_on:
      - db
      - redis
    environment:
      - DATABASE_URL=postgresql://user:password@db:5432/myapp
      - REDIS_URL=redis://redis:6379/0

  # --- Service 2: Database (Postgres) ---
  db:
    image: postgres:15
    volumes:
      - postgres_data:/var/lib/postgresql/data
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=myapp

  # --- Service 3: Redis (Cache/Broker) ---
  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"

  # --- Service 4: Reverse Proxy (Nginx) ---
  # Only needed if you are simulating the gateway locally or serving static files
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/conf.d/default.conf
    depends_on:
      - web

volumes:
  postgres_data:
```

### Nginx Middleware Config (`nginx.conf`)
Simple load balancer / reverse proxy setup.

```nginx
upstream fastapi_app {
    server web:8000;
}

server {
    listen 80;

    location / {
        proxy_pass http://fastapi_app;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

## ✅ Do's and ❌ Don'ts for Docker

| Feature | ✅ Do | ❌ Don't |
| :--- | :--- | :--- |
| **Dependencies** | Pin versions in `requirements.txt` (e.g., `fastapi==0.95.1`). | Use `pip install fastapi` without version (builds may break randomly). |
| **Docker Build** | Use multi-stage builds for production to keep images tiny. | Ship your entire source code including `.git` or tests in the final prod image. |
| **Secrets** | Use Environment Variables (pass them in `docker-compose` or k8s secrets). | Hardcode secrets in `Dockerfile` or commit `.env` files. |
| **Data** | Use Docker Volumes for persistent data (DBs). | Store data inside the container filesystem (it vanishes on restart). |
| **User** | Run container as a non-root user (create a user in Dockerfile) for security. | Run everything as root (default). |
