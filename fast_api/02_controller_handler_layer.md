# Controller / Handler Layer in FastAPI

FastAPI calls controllers "Path Operations."

## 1. Basic Path Operation
Uses standard Python type hints.

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/{item_id}")
async def read_item(item_id: int, q: str | None = None):
    return {"item_id": item_id, "q": q}
```

## 2. APIRouter (Modular Views)
Equivalent to Django apps / Blueprints.

```python
# users.py
from fastapi import APIRouter

router = APIRouter(prefix="/users", tags=["users"])

@router.get("/")
async def read_users():
    return [{"username": "Rick"}, {"username": "Morty"}]

# main.py
from fastapi import FastAPI
from . import users

app = FastAPI()
app.include_router(users.router)
```

## 3. Request Body & Status Codes
```python
from fastapi import status
from pydantic import BaseModel

class Item(BaseModel):
    name: str

@app.post("/items/", status_code=status.HTTP_201_CREATED)
async def create_item(item: Item):
    return item
```
