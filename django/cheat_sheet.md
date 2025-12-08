# Django Cheat Sheet

## 🚀 Quickstart & Setup

### Installation
```bash
pip install django
```

### Create Project & App
```bash
django-admin startproject myproject .
python manage.py startapp myapp
```
*Note: The `.` creates the project in the current directory.*

### Running the Server
```bash
python manage.py runserver
```

## 📂 Essential Configuration

### Register App (`settings.py`)
```python
INSTALLED_APPS = [
    # ...
    'myapp',
]
```

### Create a View (`myapp/views.py`)
```python
from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, world!")
```

### URL Routing (`myproject/urls.py`)
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('myapp/', include('myapp.urls')),
]
```

### App URL Routing (`myapp/urls.py`)
```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

## ✅ Do's and ❌ Don'ts

| Feature | ✅ Do | ❌ Don't |
| :--- | :--- | :--- |
| **ORM** | Use `select_related` (FK) and `prefetch_related` (M2M) to avoid N+1 problems. | Loop through a queryset in a template that triggers a DB query for every item. |
| **Settings** | Use environment variables (e.g., `python-decouple`, `django-environ`) for secrets. | Hardcode `SECRET_KEY` or DB credentials in `settings.py`. |
| **Views** | Use Class Based Views (CBVs) for standard CRUD; keep Thin Views. | Write "Fat Views" with all business logic. Put logic in Models or Services/Selectors. |
| **User Model** | Create a custom user model **before** the first migration. | Stick with the default User model if you might need to extend it later (hard to switch mid-project). |
| **Static Files** | Use `collectstatic` for production and a proper storage backend (S3, WhiteNoise). | Serve static files with Django in production (`DEBUG=True`). |

## 💡 Key Features Snippets

### Models (`myapp/models.py`)
```python
from django.db import models

class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')
    
    def __str__(self):
        return self.question_text
```

### Migrations
```bash
python manage.py makemigrations
python manage.py migrate
```

### Admin Panel
```bash
python manage.py createsuperuser
```
Register model in `myapp/admin.py`:
```python
from django.contrib import admin
from .models import Question

admin.site.register(Question)
```
