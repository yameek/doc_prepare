# Testing & Utilities in FastAPI

FastAPI provides `TestClient`, built on `httpx` (or `requests` in older versions).

## 1. TestClient
Easy synchronous testing of async endpoints.

```python
from fastapi.testclient import TestClient
from .main import app

client = TestClient(app)

def test_read_main():
    response = client.get("/")
    assert response.status_code == 200
    assert response.json() == {"msg": "Hello World"}
```

## 2. Testing Database (Pytest Fixtures)
Override the `get_session` dependency.

```python
# conftest.py
import pytest
from fastapi.testclient import TestClient
from sqlmodel import Session, SQLModel, create_engine
from .main import app, get_session

# Use in-memory DB for tests
engine = create_engine("sqlite:///:memory:")

@pytest.fixture(name="session")
def session_fixture():
    SQLModel.metadata.create_all(engine)
    with Session(engine) as session:
        yield session
    SQLModel.metadata.drop_all(engine)

@pytest.fixture(name="client")
def client_fixture(session: Session):
    def get_session_override():
        return session

    app.dependency_overrides[get_session] = get_session_override
    client = TestClient(app)
    yield client
    app.dependency_overrides.clear()
```

## 3. Async Tests (Advanced)
If you need to test async code specifically (e.g. databases), use `httpx.AsyncClient` + `pytest-asyncio`.

```python
import pytest
from httpx import AsyncClient

@pytest.mark.asyncio
async def test_root():
    async with AsyncClient(app=app, base_url="http://test") as ac:
        response = await ac.get("/")
    assert response.status_code == 200
```
