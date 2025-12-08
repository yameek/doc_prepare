# Business Logic / Service Layer in Django

Avoid "Fat Views." Keep views focused on HTTP handling (parsing request, returning response). Put core business logic in a Service Layer.

## 1. Where does logic go?
*   **Selectors**: For complex list operations/filtering (Reading data).
*   **Services**: For complex write operations (Creating/Updating data).
*   **Model Methods**: For simple logic inherent to the single object state.

## 2. Example: Booking Service

**Avoid placing this in the View `post` method:**

```python
# services.py / use_cases.py

from django.db import transaction
from .models import Booking, Payment
from .emails import send_confirmation_email

def create_booking(*, user, room, date_range):
    """
    Functional approach to business logic.
    """
    # 1. Validation Logic
    if not room.is_available(date_range):
        raise ValueError("Room is occupied")

    # 2. Transactional Logic
    with transaction.atomic():
        booking = Booking.objects.create(
            user=user,
            room=room,
            start=date_range.start,
            end=date_range.end
        )
        
        # 3. Side effects (Payment, etc)
        payment = Payment.process(booking)
        booking.mark_paid(payment)

    # 4. Async Tasks (Non-blocking)
    send_confirmation_email.delay(booking.id)

    return booking
```

## 3. Usage in View / API
The view simply orchestrates the call.

```python
# views.py
from rest_framework.views import APIView
from rest_framework.response import Response
from .services import create_booking

class BookingCreateView(APIView):
    def post(self, request):
        serializer = BookingRequestSerializer(data=request.data)
        serializer.is_valid(raise_exception=True)

        try:
            booking = create_booking(
                user=request.user, 
                **serializer.validated_data
            )
        except ValueError as e:
            return Response({"error": str(e)}, status=400)

        return Response({"id": booking.id}, status=201)
```
