# Dart Basics

Dart is a client optimized language made by Google for developing fast apps on any platform. Its main usage is to build Flutter UIs but it can also be used for servers or scripts. 

With Flutter you can build mobile, web and desktop apps.
Dart looks like a mix of Java, JavaScript and C#

## The Basics

```dart
var name = "Bob"; // Type annotaion not needed
String name = "Jonas"; // But can be added
int id = 1;
double price = 9.99;
final value = 10;
const pi = 3.14;
bool status = false;
```

### Printing

The dart command to print something is just `print();`
To print text and variables the `$` is used:

```dart
String name = "Bob";
print('Hello: $name');
```

---

### `const` vs `final`:

Both options are "cant change that later" but const is locked before the app even runs

---

### Null safety

Dart is strict when it comes to nulls. A normal variable cant be null except you tell it to be.

```dart
String name = "Bob"; // Cant be null
String? name; // The ? means it can be null
```

---

### Functions

Functions in Dart are very similar to methods in java.

There build nearly the same way:

`Return Type` + `Function Name`(`Parameters`)

With a return value: 

```dart
int add(int a, int b) {
	return a + b;
}
```

Without a return value:

```dart
void greet(String name) {
	print('Hello : $name');
}
```

---

### Classes

Dart is heavily focus on object oriented programming

Lets look at a easy Person class:

```dart
class Person {
	String name;
	int age;
	
	Person(this.name, this.age); // short constructor
	
	void greet() { // No need for a parameter
		print('Hi i am $name);
	}
}
```

```dart
var person = Person("Bob", 18);
person.greet();
```

---

### Loops and ifs

Loops and Ifs are very much the same as in Java

```dart
if (age > 10) {}

for (int i = 0; i < 5; i++) {}

for(var item in itemList) {}

while(true) {}
```

---

### Collections

```dart
var list = [1, 2, 3];

var map = {'name': 'Alex', 'age': 25};

var set = {1, 2, 3};
```

---

### Async code

Dart handles async request natively. This is very useful for API calls 

```dart
Future<String> fetchData() async {
	await Future.delayed(Duration(seconds: 1));
	return 'done';
}
```

Lets look into this code further:

- `Future` -> The return value will come later
- `<String>` -> It will be a string
- `async` -> Marks the function as asynchronous, allowing it to use `await`
- `await` -> Waits until the `Future` is complete before continuing
- `Future.delayed(Duration(seconds: 1))` → Creates a `Future` that completes after 1 second

---

## Nice to know:

Some things that dart uses that are nice to know.

### Hot reload

You can change you app / code and see the change instantly. Even if your app is only showing in the local simulator.

### Package manager

The `pubspec.yaml` is the `pom.xml` of Dart

Adding the dependency http is very simple: 
```yaml
name: cli
description: A sample command-line application.
version: 1.0.0

dependencies:
	http: ^1.4.0
```