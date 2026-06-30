# Uvicorn

Uvicorn is the service that manages the HTTP request and hands them to a python FastAPI backend
It starts and listens for requests on a specific port (for example: `8000`)

## Start Uvicorn

To start Uvicorn this command is used:

```bash
uvicorn main:app --reload
```

`main` -> File (`main.py`)
`app` -> Variable which saved the `FastAPI()` (`app = FastAPI`)
`--reload` -> Server restarts automatically after changes (Only for development)

### Important configuration options

```bash
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

`--host 0.0.0.0` -> Access from every IP (Important for docker) 
`--port 8000` -> Which port unicorn is running

So with these options you tell Uvicorn to run on `Port 8000` and accept every IP (Like localhost, Virtual Docker IP...)