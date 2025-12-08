# Packaging & Deployment in Django

## 1. WSGI Server (Gunicorn)
Do not use `runserver` in production. Use a proper WSGI server.

`pip install gunicorn`

Run:
`gunicorn myproject.wsgi:application --bind 0.0.0.0:8000`

## 2. Dockerfile
Standard containerization.

```dockerfile
FROM python:3.11-slim

WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

# Collect static files
RUN python manage.py collectstatic --noinput

CMD ["gunicorn", "myproject.wsgi:application", "--bind", "0.0.0.0:8000"]
```

## 3. Static Files in Production
WhiteNoise makes serving static files efficient from Gunicorn so you don't need Nginx just for that.

`pip install whitenoise`

**settings.py**:
```python
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'whitenoise.middleware.WhiteNoiseMiddleware', # Add here
    # ...
]

STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'
```
