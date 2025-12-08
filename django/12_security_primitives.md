# Security Primitives in Django

Django provides many security features by default.

## 1. Protections
*   **CSRF (Cross-Site Request Forgery)**: `CsrfViewMiddleware`. Requires `{% csrf_token %}` in forms.
*   **XSS (Cross-Site Scripting)**: Templates auto-escape variables by default.
*   **SQL Injection**: ORM handles parameterization automatically.

## 2. Important Settings
```python
# settings.py

# In Production:
DEBUG = False

# Cookie Security
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
SESSION_COOKIE_HTTPONLY = True # Prevent JS access

# Host headers
ALLOWED_HOSTS = ['yourdomain.com']

# HSTS (Strict Transport Security) - Force HTTPS
SECURE_HSTS_SECONDS = 31536000 # 1 year
SECURE_HSTS_INCLUDE_SUBDOMAINS = True
SECURE_SSL_REDIRECT = True
```

## 3. Rate Limiting (DRF)
Protect APIs from abuse.

```python
# settings.py
REST_FRAMEWORK = {
    'DEFAULT_THROTTLE_CLASSES': [
        'rest_framework.throttling.AnonRateThrottle',
        'rest_framework.throttling.UserRateThrottle'
    ],
    'DEFAULT_THROTTLE_RATES': {
        'anon': '100/day',
        'user': '1000/day'
    }
}
```
