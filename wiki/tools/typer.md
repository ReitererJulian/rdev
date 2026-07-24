# Typer

Typer is a library for building `CLI` applications based on python type hints.
It automatically build CLI Commands from normal python functions.

- Every function with a `@app.command` annotation is a own sub command like `/users` for a REST-API.
- Function parameters become CLI-Arguments or Options
- Typer uses type hints to validate the input (for example only numbers allowed)

## What is a CLI?

A `CLI` (Command-Line-Interface) is a way to control a program without a graphical interface just text commands. 

Instead of pressing a button you could type something like:

```bash
python main.py ping --host 127.0.0.1
```

This is a command to `ping` the `--host` with the IP `127.0.01`

## Typer Code

Now lets look at how to code a CLI-Command

```python
import typer

app = typer.Typer()

@app.command()
def ping(host: str):
	print(f"Pinging: {host}")
```