# Data Persistence in FastAPI

FastAPI is unopinionated. **SQLAlchemy** (async) is the standard choice. **SQLModel** is a modern wrapper by FastAPI's creator.

## 1. SQLModel Example (SQLAlchemy Core + Pydantic)
Combines DB models and Pydantic schemas.

```python
# models.py
from typing import Optional
from sqlmodel import Field, SQLModel, create_engine, Session

class Hero(SQLModel, table=True):
    id: Optional[int] = Field(default=None, primary_key=True)
    name: str
    secret_name: str
    age: Optional[int] = None

# db.py
sqlite_file_name = "database.db"
sqlite_url = f"sqlite:///{sqlite_file_name}"

engine = create_engine(sqlite_url)

def create_db_and_tables():
    SQLModel.metadata.create_all(engine)

def get_session():
    with Session(engine) as session:
        yield session
```

## 2. Using in Path Operations (Dependency Injection)
```python
# main.py
from fastapi import Depends, FastAPI, HTTPException
from sqlmodel import Session, select
from .db import get_session
from .models import Hero

app = FastAPI()

@app.post("/heroes/", response_model=Hero)
def create_hero(hero: Hero, session: Session = Depends(get_session)):
    session.add(hero)
    session.commit()
    session.refresh(hero)
    return hero

@app.get("/heroes/{hero_id}", response_model=Hero)
def read_hero(hero_id: int, session: Session = Depends(get_session)):
    hero = session.get(Hero, hero_id)
    if not hero:
        raise HTTPException(status_code=404, detail="Hero not found")
    return hero
```

## 3. Alembic (Migrations)
Standard for SQLAlchemy migrations.
*   `alembic init alembic`
*   Set `target_metadata` in `env.py`.
*   `alembic revision --autogenerate -m "Init"`
*   `alembic upgrade head`
