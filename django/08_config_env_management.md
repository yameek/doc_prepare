# Configuration & Env Management in Django

Never hardcode secrets. Separate config from code.

## 1. settings.py
Django's central configuration file.

## 2. Using `python-decouple` or `django-environ`
These libraries allow reading vars from a `.env` file.

**Installation**:
`pip install python-decouple`

**.env file**:
```
DEBUG=True
SECRET_KEY=super-secret-key
DATABASE_URL=postgres://user:pass@localhost:5432/mydb
ALLOWED_HOSTS=.localhost,127.0.0.1
```

**settings.py**:
```python
from decouple import config, Csv

SECRET_KEY = config('SECRET_KEY')
DEBUG = config('DEBUG', default=False, cast=bool)
ALLOWED_HOSTS = config('ALLOWED_HOSTS', cast=Csv())

# Database setup using helper (dj-database-url is popular too)
# DATABASES = { ... }
```

## 3. Splitting Settings (Advanced)
For large projects, split `settings.py` into a package:
```
settings/
    __init__.py
    base.py
    development.py
    production.py
```
Run with: `python manage.py runserver --settings=myproject.settings.development`

## 4. Static & Media Files
*   **STATIC_URL**: URL prefix (e.g., `/static/`).
*   **STATIC_ROOT**: Dir where `collectstatic` gathers files for production.
*   **MEDIA_ROOT**: Dir for user-uploaded files.

```python
# settings.py
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')

MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```
