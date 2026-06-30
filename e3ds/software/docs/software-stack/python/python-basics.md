# Python

## Basics

To output something to the console in python you use `print()`

```python
print("Hello World")
``` 

### Variables

To define variables in python, you do not need to define the datatype like in java
You can just write:

```python
# Numbers
x = 5
y = 3.14

# String
name = "Max"

# Boolean
is_true = True

# Arrays
fruits = ["Apple", "Orange"]

# List
numbers = [1, 2, 3, 4]
```

Dictionaries:

```python
user = {
    "id": 1,
    "name": "Max",
    "active": True
}

print(user["name"])      # Max
user["age"] = 25         # add key
print(user.get("email")) # None instead of error
```

#### Lists vs Sets vs Dictionary

| *Typ* | *Syntax* | *Duplicates* | *Ordered* |
|--|--|--|--|
| List | `[1, 2, 3]` | Yes | Yes |
|Set | `{1, 2, 3}` | No | No |
| Dict | `{"key": "value"} | Yes | Yes |

### If-Else

Python uses indents instead of `{}` like java

```python
age = 15

if age >= 18:
	print("Adult")
else:
	print("Minor")
``` 


### For-Loop

```python
for fruit in fruits:
	print(fruit)
	
# range
for i in range(5)
	print(i)
``` 


### While-Loop

```python
count = 0

while count < 5:
	print(count)
	count += 1
``` 

### Type Annotations

Type Annotations are used to tell the code editor what type of data you want. 
This helps you not make mistakes when defining variables

Without Type Annotations:
```python
# age should be an int
age = 10

# age can also be a string
age = "ten"
```

With Type Annotations the code editor warns you that you are using the wrong datatype.
It will not throw an error.

With Type Annotations
```python
age: int = 10

# editor highlights as wrong
age: int = "ten"
```

### Functions

Keyword `def`
No need for a return datatype like in java

```python
def greet(name):
	return "Hello " + name
	
message = greet("Max")
print(message)
``` 

```python
def add(a, b):
	return a + b #Can be int or float
	
result = add(5, 10) # result is a int 
result2 = add("Hi ", "!") # result2 is a string
``` 

It is possible to define the datatype the function expects and also what it should return

```python
# a and b need to be ints
# adding two ints will return a int 
def add(a: int, b: int) -> int:
	return a + b
	
print(add(2,2))
```

If nothing is there to return you can write `-> None:`
Also default values can be added using `=`

```python
# Hi is now a default value
def greet(name: str, greeting: str = "Hi" ) -> None:
	print(f"{greeting}, {name}!")
	
greet("Bob", "Servas") # Servas, Bob!
greet("Hans") # Hi, Hans
```

### F-Strings

The F stands for Formatted String.
It makes printing including variables a lot simpler and easier

Without F-String
```python
name: str = "Bob"
age: int = 10

print("Name:" + name + ", Age:" + age)
```

With F-String

```python
name: str = "Bob"
age: int = 10

print(f"Name: {name}, Age: {age}")
```

### Project Structure

Backend structure

```
backend/
├── app/
│   ├── __init__.py
│   ├── main.py              # FastAPI() app, include_router(...)
│   ├── routers/
│   │   ├── __init__.py
│   │   └── user_router.py   # @router.get("/users")
│   ├── services/
│   │   ├── __init__.py
│   │   └── user_service.py  # Business-Logik
│   ├── models/
│   │   ├── __init__.py
│   │   └── user.py          # Model classes
│   └── core/
│       ├── __init__.py
│       ├── config.py        # reads .env, settings
│       └── database.py      # DB-Connection
├── tests/
│   └── test_users.py
├── .env.example
├── .env                      # NOT in Git!
├── Dockerfile
├── pyproject.toml
└── uv.lock
```

### Classes

Classes in python are similar to classes in java.

```python
class User:
	# Attributes
	name: str
	age: int
	
	# Constructor
	def __init__(self, name: str, age: int):
		self.name = name
		self.age = age
```

Create a `User` object:

```python
user = User("Bob", 18)

print(user.name)
print(user.age)
```
