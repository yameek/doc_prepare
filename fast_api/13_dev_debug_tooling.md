# Dev & Debug Tooling in FastAPI

## 1. Interactive Documentation
FastAPI automatically generates docs.
*   **Swagger UI**: `/docs` (Interactive testing)
*   **ReDoc**: `/redoc` (Clean documentation)

## 2. Debugging with PDB/IPDB
Since you run Uvicorn from the terminal, standard breakpoints work.

`python3 -m pip install ipdb`

```python
@app.get("/")
def read_root():
    import ipdb; ipdb.set_trace()
    return {"Hello": "World"}
```

## 3. Override Dependencies
Great for isolating parts of the app during dev/testing (see Testing section).

`app.dependency_overrides = {}`
