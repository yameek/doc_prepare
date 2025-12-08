# Request-Response Lifecycle in FastAPI

FastAPI is built on Starlette (ASGI toolkit) and Pydantic.

## Overview
1.  **ASGI Server (Uvicorn)**: Receives raw socket data.
2.  **Middleware**: Global interceptors.
3.  **Router**: Matches path to operation function.
4.  **Dependencies**: Runs before the path operation (validation, db session).
5.  **Path Operation**: Main logic.

## 1. Middleware
Using `@app.middleware("http")` or adding BaseHTTPMiddleware.

```python
import time
from fastapi import FastAPI, Request

app = FastAPI()

@app.middleware("http")
async def add_process_time_header(request: Request, call_next):
    start_time = time.time()
    
    response = await call_next(request)
    
    process_time = time.time() - start_time
    response.headers["X-Process-Time"] = str(process_time)
    
    return response
```

## 2. Lifespan Events
Execute code on startup/shutdown.

```python
from contextlib import asynccontextmanager

@asynccontextmanager
async def lifespan(app: FastAPI):
    # Startup: Load ML models, connect to DB
    print("Startup")
    yield
    # Shutdown: Close connections
    print("Shutdown")

app = FastAPI(lifespan=lifespan)
```
