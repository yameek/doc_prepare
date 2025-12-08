# Error Handling & Logging in Django

## 1. Exception Handling
Django translates unhandled exceptions into 500 pages (or debug pages in Dev). In APIs, you want structured JSON errors.

### DRF Custom Exception Handler
Standardize API error responses.

```python
# utils/exceptions.py
from rest_framework.views import exception_handler

def custom_exception_handler(exc, context):
    # Call core REST framework handler first to get the standard error response.
    response = exception_handler(exc, context)

    if response is not None:
        custom_data = {
            'status': 'error',
            'code': response.status_code,
            'details': response.data
        }
        response.data = custom_data

    return response
```

**Settings**:
```python
REST_FRAMEWORK = {
    'EXCEPTION_HANDLER': 'myproject.utils.exceptions.custom_exception_handler'
}
```

## 2. Logging Configuration
Django uses Python's standard `logging` dictConfig.

```python
# settings.py

LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'formatters': {
        'verbose': {
            'format': '{levelname} {asctime} {module} {message}',
            'style': '{',
        },
        'simple': {
            'format': '{levelname} {message}',
            'style': '{',
        },
    },
    'handlers': {
        'console': {
            'class': 'logging.StreamHandler',
            'formatter': 'simple',
        },
        'file': {
            'level': 'ERROR',
            'class': 'logging.FileHandler',
            'filename': 'django_errors.log',
            'formatter': 'verbose',
        },
    },
    'loggers': {
        'django': {
            'handlers': ['console', 'file'],
            'level': 'INFO',
            'propagate': True,
        },
        'myapp': {  # Your custom app logger
            'handlers': ['console'],
            'level': 'DEBUG',
        }
    },
}
```

**Usage**:
```python
import logging
logger = logging.getLogger(__name__)

def my_view(request):
    try:
        # ... logic
        logger.info("Processing request")
    except Exception as e:
        logger.error(f"Something went wrong: {e}", exc_info=True)
```
