# Validation & Serialization in FastAPI

FastAPI validation is powered by **Pydantic**.

## 1. Pydantic Models
Validation logic lives in the model.

```python
from pydantic import BaseModel, EmailStr, Field, validator

class UserCreate(BaseModel):
    username: str
    email: EmailStr
    password: str = Field(min_length=8)
    age: int = Field(gt=0, lt=120)

    # Custom validator
    @validator('username')
    def username_alphanumeric(cls, v):
        if not v.isalnum():
            raise ValueError('must be alphanumeric')
        return v
```

## 2. Request & Response Models
FastAPI filters response data based on the `response_model`.

```python
class UserOut(BaseModel):
    username: str
    email: EmailStr
    # password is NOT here, so it won't be sent back

@app.post("/users/", response_model=UserOut)
async def create_user(user: UserCreate):
    # logic to save user
    return user # Pydantic will strip 'password'
```

## 3. Query & Path Parameters
Validation works for URL params too.

```python
from fastapi import Query

@app.get("/items/")
async def read_items(
    q: str | None = Query(default=None, min_length=3, max_length=50)
):
    results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}
    if q:
        results.update({"q": q})
    return results
```
