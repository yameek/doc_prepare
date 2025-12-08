# Business Logic / Service Layer in FastAPI

FastAPI's **Dependency Injection (DI)** system is perfect for service layers.

## 1. Defining a Service
Encapsulate logic in a class or function.

```python
# services.py
class NotificationService:
    def send_email(self, email: str, message: str):
        print(f"Sending email to {email}: {message}")

class OrderService:
    def __init__(self, notifier: NotificationService):
        self.notifier = notifier

    def create_order(self, user_email: str, item: str):
        # Logic...
        self.notifier.send_email(user_email, f"Order {item} created")
        return {"status": "created"}
```

## 2. Using Dependency Injection
Inject the service into your path operation.

```python
# dependencies.py
def get_notification_service():
    return NotificationService()

def get_order_service(
    notifier: NotificationService = Depends(get_notification_service)
):
    return OrderService(notifier)

# main.py
@app.post("/orders/")
async def create_order(
    item: str, 
    email: str, 
    service: OrderService = Depends(get_order_service)
):
    return service.create_order(email, item)
```

## 3. Why?
*   **Testability**: You can easily override `get_order_service` in tests with a mock.
*   **Decoupling**: The view (path operation) doesn't need to know how to construct the service.
