# Background Jobs in FastAPI

## 1. Built-in BackgroundTasks
For simple, fire-and-forget tasks that run in the same process after the response is sent.

```python
from fastapi import BackgroundTasks, FastAPI

app = FastAPI()

def write_notification(email: str, message: str):
    with open("log.txt", "a") as mode:
        mode.write(f"notification for {email}: {message}\n")

@app.post("/send-notification/{email}")
async def send_notification(email: str, background_tasks: BackgroundTasks):
    background_tasks.add_task(write_notification, email, message="some notification")
    return {"message": "Notification sent in the background"}
```

## 2. Heavy Jobs (Celery / ARQ)
For CPU-heavy or mission-critical tasks, use a separate worker.

**Celery Example**: Same as Django, just import the logic.

```python
# worker.py
from celery import Celery
celery = Celery(__name__, broker="redis://localhost:6379/0")

@celery.task
def heavy_task(word: str):
    return f"Processed {word}"

# main.py
from .worker import heavy_task

@app.post("/process")
async def process(word: str):
    heavy_task.delay(word)
    return {"message": "Processing started"}
```
