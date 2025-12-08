# Request-Response Lifecycle in Django

This guide covers how Django handles an incoming HTTP request and returns a response.

## Overview
1.  **WSGI/ASGI Handler**: Entry point for the web server (Gunicorn/Uvicorn).
2.  **Middleware**: Global hooks that process requests before they reach the view and responses before they leave.
3.  **URL Routing (URLConf)**: Maps URL paths to Python callback functions (Views).
4.  **View**: Logic that processes the request and returns a response.

## 1. Middleware
Middleware is efficient for cross-cutting concerns like Auth, Logging, CORS.

```python
# myapp/middleware.py

import time
import logging

logger = logging.getLogger(__name__)

class TimingMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        # Code to be executed for each request before
        # the view (and later middleware) are called.
        start_time = time.time()

        response = self.get_response(request)

        # Code to be executed for each request/response after
        # the view is called.
        duration = time.time() - start_time
        logger.info(f"Request {request.path} took {duration:.2f}s")
        
        # Add a custom header
        response['X-Process-Time'] = str(duration)

        return response
```

**Registration in `settings.py`**:
```python
MIDDLEWARE = [
    # ...
    'myapp.middleware.TimingMiddleware',
]
```

## 2. URL Routing
Django keeps URL configuration separate from views, allowing for cleaner separation.

```python
# myproject/urls.py
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/v1/', include('api.urls')), # Modular routing
]

# api/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('users/', views.UserListView.as_view(), name='user-list'),
    path('users/<int:pk>/', views.UserDetailView.as_view(), name='user-detail'),
]
```

## 3. WSGI vs ASGI
*   **WSGI**: Synchronous, standard for most Django apps.
*   **ASGI**: Asynchronous, required for Django Channels (WebSockets) or `async def` views.
