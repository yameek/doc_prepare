# Authentication & Authorization in Django

Django ships with a robust user authentication system (`django.contrib.auth`).

## 1. Built-in Authentication
Handles User sessions, hashing (PBKDF2), and login/logout views.

```python
# settings.py
AUTH_USER_MODEL = 'myapp.CustomUser' # Recommended to set this at start of project

# views.py
from django.contrib.auth.decorators import login_required

@login_required # Traditional Login
def my_protected_view(request):
    user = request.user
    # ...
```

## 2. Permissions (RBAC)
Django has a built-in permissions system (Group, Permission models).

```python
from django.contrib.auth.mixins import PermissionRequiredMixin

class MyView(PermissionRequiredMixin, View):
    permission_required = 'app.add_product'
```

## 3. JWT Authentication (DRF)
For modern SPAs/Mobile Apps, use JSON Web Tokens via `djangorestframework-simplejwt`.

```python
# settings.py
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    )
}

# urls.py
from rest_framework_simplejwt.views import (
    TokenObtainPairView,
    TokenRefreshView,
)

urlpatterns = [
    path('api/token/', TokenObtainPairView.as_view(), name='token_obtain_pair'),
    path('api/token/refresh/', TokenRefreshView.as_view(), name='token_refresh'),
]

# views.py
from rest_framework.permissions import IsAuthenticated
from rest_framework.views import APIView

class ProtectedDataView(APIView):
    permission_classes = [IsAuthenticated]

    def get(self, request):
        return Response(content={"message": "Hello authenticated user!"})
```

## 4. Custom Permissions
```python
# permissions.py
from rest_framework import permissions

class IsOwner(permissions.BasePermission):
    """
    Custom permission to only allow owners of an object to edit it.
    """
    def has_object_permission(self, request, view, obj):
        # Read permissions are allowed to any request,
        # so we'll always allow GET, HEAD or OPTIONS requests.
        if request.method in permissions.SAFE_METHODS:
            return True

        # Write permissions are only allowed to the owner.
        return obj.owner == request.user
```
