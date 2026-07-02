# Async vs Sync

The problem that needs to be fixed is that some request can take some time and block the server and freeze the application.
To fix this we need `Async-Requests`.

## Synchronized

When sending this specific ping request the server waits for 2 seconds, blocking all other traffic from continuing and freezing the app for the 2 seconds.

```python
import time

@app.get("/sync/ping")
def sync_ping():
	time.sleep(2)
	return {"message": "pong"}
```

To avoid this `Asynchronous Request` are used.

## Asynchronous Request

```python
import asyncio

@app.get("/async/ping")
async def async_ping():
	await asyncio.sleep(2)
	return {"message": "pong"}
```

`await` -> I wait here, in the meantime you can do other things

`await` only works inside an `async def` function, and only with things that support it ("awaitables").
