# Background Jobs in Django

Use **Celery** for asynchronous task queues (email, processing, scheduled tasks).

## 1. Celery Setup

`pip install celery redis`

**myproject/celery.py**:
```python
import os
from celery import Celery

# Set default Django settings module
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'myproject.settings')

app = Celery('myproject')

# Read config from settings.py with prefix 'CELERY_'
app.config_from_object('django.conf:settings', namespace='CELERY')

# Load task modules from all registered Django app configs.
app.autodiscover_tasks()
```

**myproject/\_\_init\_\_.py**:
```python
from .celery import app as celery_app
__all__ = ('celery_app',)
```

## 2. Defining Tasks

```python
# myapp/tasks.py
from celery import shared_task

@shared_task
def add(x, y):
    return x + y

@shared_task
def send_welcome_email(user_id):
    from django.contrib.auth.models import User
    user = User.objects.get(pk=user_id)
    # ... logic to send email
```

## 3. Calling Tasks
```python
# In a view
from .tasks import send_welcome_email

def signup(request):
    # ... save user ...
    # Call async
    send_welcome_email.delay(user.id) 
    return HttpResponse("Signup complete")
```

## 4. Periodic Tasks (Celery Beat)
Schedule regular tasks.

```python
# settings.py
from celery.schedules import crontab

CELERY_BEAT_SCHEDULE = {
    'cleanup-every-night': {
        'task': 'myapp.tasks.cleanup_db',
        'schedule': crontab(hour=0, minute=0),
    },
}
```
