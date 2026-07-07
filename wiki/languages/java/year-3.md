# Jahr 3

## Inhaltsverzeichnis
* [Stream API](#stream-api)
* [Lambda](#lambda)
* [Path Klasse](#path-klasse)
* [Files Klasse](#files-klasse)
* [Java-IO und try-with-resources](#java-io-und-try-with-resources)
* [JUnit](#junit)

---

## Stream API

Die `Stream API` wird genutzt, um Sammlungen wie Lists und Sets mit weniger Code effektiv zu filtern, zu ändern und zu sortieren – anstatt For-Schleifen zu nutzen.
<br>

---

## Lambda

Ist eine verkürzte Schreibweise einer Methode. Ersetzt `anonyme Klassen`.

```
(Parameter) -> { Anweisungen }
(a, b) -> a + b
```

Geht auch mehrzeilig:
```java
(a, b) -> {
    int summe = a + b;
    return summe;
}
```
`Lambdas` kann man auch mit Listen verwenden. Das macht es einfacher, Listen zu iterieren, auszugeben und zu verändern / sortieren. Um es noch simpler zu halten, kann man `Lambdas` mit `Streams` kombinieren.

Liste ausgeben:
```java
List<String> nameList = List.of(
    "Anna",
    "Bernd"
);

nameList.forEach(n -> System.out.println(n));
```
<br>

Liste sortieren (Comparator):
```java
nameList.sort((a, b) -> a.compareTo(b));
```
<br>

Mit Streams kombinierbar:
```java
nameList.stream()
    .filter(n -> n.startsWith("A"))
    .forEach(System.out::println);
```
<br>

---

## Path Klasse

Wird verwendet, um Dateipfade oder Verzeichnisse zu repräsentieren. Ist Teil des `java.nio.file`-Pakets. Ein `Path` ist kein tatsächliches Dateihandling, sondern nur ein Verweis auf einen Speicherort.

Beispiel, um eine Datei in einem Ordner zu finden:
```java
Path base = Path.of("data");
Path file = base.resolve("test.txt");
```
Das `Working Directory` (`base`) ist der Startpunkt. Ausgehend davon wird mit `base.resolve()` geprüft, ob die Datei `test.txt` im Ordner `base` existiert.

Die `Path`-Klasse wird auch verwendet, um Pfade `absolut` zu machen.
Das heißt, aus dem relativen Pfad `Project/Folder/File` (bezogen auf das `Projekt`/`Working Directory`) wird ein `absoluter Pfad`: `C:/Users/IntelliJ/Project/Folder/File`. Dieser ist der genaue Speicherort.

Die Methode `normalize()` entfernt redundante Zeichen wie `.` oder `..`.
Also wird aus `C:/Users/../Docs` -> `C:/Docs`.
<br>

---

## Files Klasse

Die `Files`-Klasse (ebenfalls in `java.nio.file`) stellt weitere nützliche, `statische` Methoden bereit.
Diese ermöglichen einfacheres Arbeiten mit Dateien. Die Hauptaufgaben sind:
* Dateien lesen / schreiben
* prüfen, ob eine `Datei` / ein `Ordner` existiert
* kopieren, löschen, erstellen usw.

Die `Files`-Klasse und die `Path`-Klasse gehören zusammen!

Hier ein Beispiel zum Prüfen, ob eine Datei existiert:
```java
if (!Files.exists(path))
{
    Files.createFile(path);
}
```
<br>

---

## Java-IO und try-with-resources

`Java IO` bedeutet Java Input / Output und stammt aus `java.io`. Es enthält ältere Klassen zum `Einlesen` und `Schreiben` von Dateien.
Die zwei meistbenutzten sind:
`BufferedReader` zum Einlesen von Dateien,
`BufferedWriter` zum Schreiben von Dateien.

`try-with-resources` sorgt dafür, dass Ressourcen automatisch geschlossen werden, sobald man sie nicht mehr braucht.
Das ist besonders nützlich bei:
* `Reader`, `Writer`
* `Streams`

Dadurch muss man keinen `finally`-Block schreiben, um Ressourcen zu schließen.

Hier jeweils ein Beispiel zur Benutzung:

`BufferedReader` mit `try-with-resources`:
```java
try (BufferedReader br = Files.newBufferedReader(path))
{
    System.out.println(br.readLine());
} catch (IOException e)
{
    e.printStackTrace();
}
```

`BufferedWriter` mit `try-with-resources`:
```java
try (BufferedWriter br = Files.newBufferedWriter(path))
{
    br.write("Hello");
    br.newLine();
} catch (IOException e)
{
    e.printStackTrace();
}
```
<br>

---

## JUnit

`JUnit` wird benutzt, um Java-Tests zu schreiben und auszuführen, um zu überprüfen, ob Methoden richtig funktionieren.
Die Ordnerstruktur muss gleich aufgebaut sein!

```
src
 -> main
    -> java
        -> myPackage
            - Addition
 -> test
    -> java
        -> myPackage
            - AdditionTest
```

`Addition`:
```java
public class Addition
{
    public int addition(int a, int b)
    {
        return a + b;
    }
}
```
<br>

`AdditionTest`:
```java
public class AdditionTest
{
    @Test
    public void testAddition()
    {
        Addition add = new Addition();

        assertEquals(5, add.addition(2, 3));
    }
}
```

Hier wird geprüft, ob 2 + 3 gleich 5 ist.
