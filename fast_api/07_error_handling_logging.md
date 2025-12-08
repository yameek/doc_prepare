# Error Handling & Logging in FastAPI

## 1. HTTPException
Standard way to return errors.

```python
from fastapi import HTTPException, status

@app.get("/items/{item_id}")
async def read_item(item_id: str):
    if item_id == "not_found":
        raise HTTPException(
            status_code=status.HTTP_404_NOT_FOUND, 
            detail="Item not found",
            headers={"X-Error": "There goes my error"}
        )
```

## 2. Global Exception Handlers
Catch custom exceptions globally.

```python
from fastapi import Request
from fastapi.responses import JSONResponse

class UnicornException(Exception):
    def __init__(self, name: str):
        self.name = name

@app.exception_handler(UnicornException)
async def unicorn_exception_handler(request: Request, exc: UnicornException):
    return JSONResponse(
        status_code=418,
        content={"message": f"Oops! {exc.name} did something. There goes a rainbow..."},
    )
```

## 3. Logging
FastAPI (Uvicorn) uses standard Python logging. Use a structured logger like `structlog` or `loguru` for best results.

```python
import logging

logger = logging.getLogger("uvicorn")

@app.get("/")
async def root():
    logger.info("Root endpoint accessed")
    return {"message": "Hello World"}
```
