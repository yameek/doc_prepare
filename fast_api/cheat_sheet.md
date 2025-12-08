# FastAPI Cheat Sheet

## 🚀 Quickstart & Setup

### Installation
```bash
pip install fastapi "uvicorn[standard]"
```

### Minimal "Hello World"
Create `main.py`:
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "World"}
```

### Running the App
```bash
uvicorn main:app --reload
```
- Access docs at: `http://127.0.0.1:8000/docs`
- Access ReDoc at: `http://127.0.0.1:8000/redoc`

## 📂 Project Structure (Recommended)
```
/my_project
    /app
        __init__.py
        main.py
        dependencies.py
        /routers
            users.py
            items.py
        /models
        /schemas
        /core
            config.py
```

### Router Example (`app/routers/users.py`)
```python
from fastapi import APIRouter

router = APIRouter()

@router.get("/users/", tags=["users"])
async def read_users():
    return [{"username": "Rick"}, {"username": "Morty"}]
```

### Main App with Router (`app/main.py`)
```python
from fastapi import FastAPI
from .routers import users

app = FastAPI()

app.include_router(users.router)
```

## ✅ Do's and ❌ Don'ts

| Feature | ✅ Do | ❌ Don't |
| :--- | :--- | :--- |
| **Async** | Use `async def` for I/O bound tasks (DB, API calls). | Use `async def` for blocking CPU bound tasks without `run_in_executor`. |
| **Pydantic** | Use Pydantic models for request/response validation. | Manual validation inside the path operation function. |
| **Dependencies** | Use `Depends` for shared logic (DB sessions, auth). | Instantiate heavy objects globally or inside endpoints repeatedly. |
| **Status Codes** | explicit status codes `status_code=status.HTTP_201_CREATED`. | Return generic 200 OK for everything (even errors). |
| **Blocking Code** | Use `def` (not async) if using blocking libraries. | Use `async def` with blocking libraries like `requests` or standard `open()`. |

## 💡 Key Features Snippets

### Path Parameters & Validation
```python
from fastapi import Path

@app.get("/items/{item_id}")
async def read_item(item_id: int = Path(..., title="The ID of the item", ge=1)):
    return {"item_id": item_id}
```

### Request Body (Pydantic)
```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    price: float
    is_offer: bool = None

@app.put("/items/{item_id}")
async def update_item(item_id: int, item: Item):
    return {"item_name": item.name, "item_id": item_id}
```
