# Realtime Communication in Django

Use **Django Channels** to handle WebSockets. Requires ASGI.

## 1. Setup
`pip install channels`

**settings.py**:
```python
INSTALLED_APPS = [
    'daphne', # Must be first
    'channels',
    # ...
]

ASGI_APPLICATION = 'myproject.asgi.application'
```

## 2. Consumers (Event Handlers)
Comparable to Views, but for long-lived connections.

```python
# myapp/consumers.py
import json
from channels.generic.websocket import AsyncWebsocketConsumer

class ChatConsumer(AsyncWebsocketConsumer):
    async def connect(self):
        self.room_name = "general"
        self.room_group_name = f"chat_{self.room_name}"

        # Join room group
        await self.channel_layer.group_add(
            self.room_group_name,
            self.channel_name
        )
        await self.accept()

    async def disconnect(self, close_code):
        # Leave room group
        await self.channel_layer.group_discard(
            self.room_group_name,
            self.channel_name
        )

    # Receive message from WebSocket
    async def receive(self, text_data):
        text_data_json = json.loads(text_data)
        message = text_data_json['message']

        # Send message to room group
        await self.channel_layer.group_send(
            self.room_group_name,
            {
                'type': 'chat_message',
                'message': message
            }
        )

    # Receive message from room group
    async def chat_message(self, event):
        message = event['message']
        # Send message to WebSocket
        await self.send(text_data=json.dumps({'message': message}))
```

## 3. Routing
```python
# myapp/routing.py
from django.urls import re_path
from . import consumers

websocket_urlpatterns = [
    re_path(r'ws/chat/general/$', consumers.ChatConsumer.as_asgi()),
]
```
