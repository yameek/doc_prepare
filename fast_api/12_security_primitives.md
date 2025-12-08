# Security Primitives in FastAPI

## 1. CORS (Cross-Origin Resource Sharing)
Middleware to allow browser requests from different domains.

```python
from fastapi.middleware.cors import CORSMiddleware

origins = [
    "http://localhost.tiangolo.com",
    "https://localhost.tiangolo.com",
    "http://localhost",
    "http://localhost:8080",
]

app.add_middleware(
    CORSMiddleware,
    allow_origins=origins,
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

## 2. TrustedHostMiddleware
Protect against Host Header attacks.

```python
from fastapi.middleware.trustedhost import TrustedHostMiddleware

app = FastAPI()

app.add_middleware(
    TrustedHostMiddleware, 
    allowed_hosts=["example.com", "*.example.com"]
)
```

## 3. SQL Injection
Using SQLAlchemy/SQLModel variables (`session.add(hero)`) automatically handles parameterization, preventing injection. avoid raw strings for queries.
