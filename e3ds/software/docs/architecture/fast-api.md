# FastAPI

FastAPI is a simple way to build a modern Python REST APIs


```python
# main.py
from fastapi import FastAPI

app = FastAPI()

@app.get("/api/ping")
def ping():
	return {"pong"}
``` 


It also supports a simple version DI (Dependency injection) using `Depends()`
Using this you can tell FastAPI you need a Database Object and it creates one for you

```python
# main.py
from fastapi import FastAPI

app = FastAPI()

def get_db():
	return Database()

@app.get("/api/users")
def get_users(db=Depends(get_db)):
	return UserService(db).get_all()
```
