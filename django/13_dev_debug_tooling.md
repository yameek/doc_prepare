# Dev & Debug Tooling in Django

## 1. Django Debug Toolbar
Essential for optimizing queries and inspecting requests.

`pip install django-debug-toolbar`

**settings.py**:
```python
INSTALLED_APPS = [
    # ...
    'debug_toolbar',
]

MIDDLEWARE = [
    'debug_toolbar.middleware.DebugToolbarMiddleware',
    # ...
]

INTERNAL_IPS = [
    '127.0.0.1',
]
```

**urls.py**:
```python
if settings.DEBUG:
    import debug_toolbar
    urlpatterns += [
        path('__debug__/', include(debug_toolbar.urls)),
    ]
```

## 2. Django Extensions (Shell Plus)
Enhanced shell with auto-imports.

`pip install django-extensions`

Usage:
`python manage.py shell_plus`

## 3. Silk
Profiling tool for Django (checking query performance and request time).

`pip install django-silk`

Enable middleware and add to `INSTALLED_APPS`. Go to `/silk/` to view report.
