# Configuration & Env Management in FastAPI

Use **Pydantic Settings** (`pydantic-settings`).

## 1. Settings Schema
Define your configuration as a Pydantic model. Reads from env vars automatically.

`pip install pydantic-settings`

```python
# config.py
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    app_name: str = "My FastAPI App"
    admin_email: str
    items_per_user: int = 50
    
    # Nested config? Use a separate class or prefix
    # database_url reads from DATABASE_URL env var
    database_url: str 

    class Config:
        env_file = ".env"

settings = Settings()
```

## 2. Usage
Ideally, inject settings via Depends or import globally if they are static.

```python
# main.py
from functools import lru_cache
from fastapi import Depends
from .config import Settings

@lru_cache()
def get_settings():
    return Settings()

@app.get("/info")
async def info(settings: Settings = Depends(get_settings)):
    return {
        "app_name": settings.app_name,
        "admin_email": settings.admin_email,
    }
```

The `@lru_cache` ensures we only read the `.env` file once.
