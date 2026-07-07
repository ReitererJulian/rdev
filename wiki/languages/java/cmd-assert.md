# CMD & Assert

## Inhaltsverzeichnis
* [Ausführen in CMD](#ausführen-in-cmd)
* [Was heißt assert?](#was-heißt-assert)

---

## Ausführen in CMD

In den Ordner wechseln mit `cd` und `dir`, dann die Datei finden und mit `javac "filename.java"` kompilieren.
Dadurch entsteht eine `.class`-Datei, die man dann mit `java FileName` ausführen kann.

---

## Was heißt assert?

Ein `assert` vergleicht zwei Dinge: einmal das erwartete Ergebnis und das, was tatsächlich vom Programm zurückgegeben wurde. Wenn beide Werte gleich sind, besteht der Test. Wenn nicht, schlägt er fehl.

```java
assertEquals(8, Main.add(3, 5));
```
Erwartet, dass 3+5 gleich 8 ist. Wenn ja (`Main.add(3,5)` = 8), dann ist der Test `true`.
Wenn es nicht 8 ist, dann ist der Test `false`.
<br>
