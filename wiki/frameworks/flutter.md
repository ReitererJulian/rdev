# Flutter

Flutter is a toolkit used for building apps.
The tools in the toolkit are called `widgets`.

## What is a widget?

> "Everything is a widget"

There are many different types of widgets. Here are a few:

* **Buttons**
* **Text Input**
* **Lists**

The list goes on.

---

### Widget Hierarchy

Widgets can also be made up of other widgets. Let's think of a book for example. It is also built up of many things:

`Book` -> `Chapters` -> `Paragraphs` -> `Sentences` -> `Words` -> `Letters` -> `Pixels`

But it is not required to write a book like that. Something will always be different from book to book.

The same works with widgets. They can be used and formed however to build your app.

Lets look at a easy example:

This is the `AppBar`. It is the header bar for many apps.

```dart
AppBar(
	title: Text("Title Bar!"), // Text in the middle
	leading: Icon(Icons.menu), // Icon on the side
)
```

This simple widget already uses two other widgets.

It uses the:

* **Text-Widget**
* **Icon-Widget**

---

### Figure out layout and groups

So now that you know what widgets are, you could design your first layout and figure out how the different widgets are related to each other.

It could look something like this simple layout for a To-Do application. 

```bash
---------------------
|     App Bar       |
---------------------
|      Text         |
---------------------
|   Progress Bar    |
---------------------
| Checkbox | | Task |
---------------------
| Checkbox | | Task |
---------------------
| Checkbox | | Task |
---------------------
```

The widgets can be looked at as groups.

We have the `App Bar` which is a group of its own called `App Title`.
Then we have the `Body` with these widgets included: `Text`, `Progress Bar` and the `Checkboxes` and `Tasks`
The body can be further split down into a `Progress` section and a `Task` section

Now lets think of how to layout these widgets using other widgets

A so called `column` is used to arrange its children widgets vertically (Top to bottom) 
A so called `row` is used to arrange its children widgets horizontally (Left to right)

Using this the layout becomes much easier.

---

 For example:

`Column` -> `Text` and `Progress Bar`
`Rows` -> `Checkboxes` and `Tasks`

### Dart

Dart is the language used to model the application.

This code imports the basic widgets and with `void main() => runApp()` we can set the root widget when the app starts.

```dart
import 'package:flutter/material.dart';

void main() => runApp(
	Center(child: Text('Hello World')),
	); // Root widget will be defined here 
```