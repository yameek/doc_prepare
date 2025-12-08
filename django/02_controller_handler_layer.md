# Controller / Handler Layer in Django (Views)

In Django, the "Controller" logic generally lives in the **View**.

## 1. Function-Based Views (FBV)
Simple, readable, functional. Good for simple APIs or custom logic.

```python
from django.http import JsonResponse
from django.views.decorators.http import require_http_methods

@require_http_methods(["GET"])
def health_check(request):
    return JsonResponse({"status": "ok", "message": "System operational"})
```

## 2. Class-Based Views (CBV)
Good for CRUD, reusing logic via inheritance (Mixins).

```python
from django.views import View
from django.http import HttpResponse

class MyCustomView(View):
    def get(self, request):
        return HttpResponse('Result of GET')

    def post(self, request):
        return HttpResponse('Result of POST')
```

## 3. Django REST Framework (DRF) ViewSets
The standard for building APIs. Combines logic for a set of related views.

```python
from rest_framework import viewsets
from rest_framework.response import Response
from rest_framework.decorators import action
from django.contrib.auth.models import User
from .serializers import UserSerializer

class UserViewSet(viewsets.ModelViewSet):
    """
    A viewset that provides the standard actions:
    list, create, retrieve, update, partial_update, destroy.
    """
    queryset = User.objects.all()
    serializer_class = UserSerializer

    # Custom action: /api/users/recent/
    @action(detail=False, methods=['get'])
    def recent(self, request):
        recent_users = self.queryset.order_by('-date_joined')[:5]
        serializer = self.serializer_class(recent_users, many=True)
        return Response(serializer.data)
```
