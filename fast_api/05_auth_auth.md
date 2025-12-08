# Authentication & Authorization in FastAPI

FastAPI provides security utilities (OAuth2 scopes) but doesn't enforce a specific user model or DB.

## 1. OAuth2 Password Bearer (JWT)
Standard pattern: Client sends `username` & `password` to `/token`, gets `access_token`, sends token in `Authorization` header.

## 2. Token Endpoint
```python
from fastapi import Depends, HTTPException, status
from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm
from passlib.context import CryptContext
from jose import JWTError, jwt

SECRET_KEY = "SECRET"
ALGORITHM = "HS256"

pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")
oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

# Verify Password
def verify_password(plain_password, hashed_password):
    return pwd_context.verify(plain_password, hashed_password)

# Generate Token
def create_access_token(data: dict):
    return jwt.encode(data, SECRET_KEY, algorithm=ALGORITHM)

@app.post("/token")
async def login(form_data: OAuth2PasswordRequestForm = Depends()):
    user = get_user(form_data.username) # Your generic get_user function
    if not user or not verify_password(form_data.password, user.hashed_password):
        raise HTTPException(status_code=400, detail="Incorrect username or password")
    
    token = create_access_token(data={"sub": user.username})
    return {"access_token": token, "token_type": "bearer"}
```

## 3. Protecting Routes (Current User)
```python
async def get_current_user(token: str = Depends(oauth2_scheme)):
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        username: str = payload.get("sub")
        if username is None:
            raise HTTPException(status_code=401)
    except JWTError:
        raise HTTPException(status_code=401)
    
    user = get_user(username)
    return user

@app.get("/users/me")
async def read_users_me(current_user: User = Depends(get_current_user)):
    return current_user
```
