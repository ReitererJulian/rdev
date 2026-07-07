# Creational Design Patterns

## Inhaltsverzeichnis
* [Was sind Design Patterns?](#was-sind-design-patterns)
* [Singleton](#singleton)
* [Builder](#builder)
* [Abstract Factory](#abstract-factory)

---

## Was sind Design Patterns?

`Design Patterns` sind Lösungen für wiederkehrende Programmierprobleme.
Sie helfen, den Code sauber und leicht wartbar zu halten.

Man kann sich Design Patterns wie `Baupläne` vorstellen, mit denen man typische Aufgaben immer wieder ähnlich löst.
Solche Aufgaben wären:
* Erstellen von Objekten
* Zusammenarbeiten von Klassen
* Organisation von Datenflüssen

<br>

Diese Kategorie von `Design Patterns` befasst sich damit, wie Objekte erstellt (instanziiert) werden.

Diese Design Patterns lösen folgende Probleme:
* Wie stelle ich sicher, dass nur ein Objekt einer Klasse existiert?
* Wie kann ich die Erstellung von Objekten kapseln oder vereinfachen?

Die drei wichtigsten sind:
* `Singleton`
* `Builder`
* `Abstract Factory`

---

## Singleton

Das `Singleton`-Pattern sorgt dafür, dass nur eine einzige Instanz (Objekt) einer Klasse existiert und man von überall darauf zugreifen kann.
Also einen zentralen `Zugriffspunkt` auf diese Instanz.
Das ist nützlich für Dinge, die nur einmal pro Programm existieren sollen, z.B.:
* `Datenbankverbindung`
* `Logger`
* `Konfigurationen`

Wenn man diese Objekte öfter erstellt, kann das zu `Inkonsistenzen` oder unnötiger Ressourcenbelastung führen.

<br>

**Vorteile:**
* Kontrollierter Zugriff auf eine Instanz im gesamten System
* Spart Ressourcen
* Global zugänglich

**Nachteile:**
* Nicht automatisch `Multi-Thread-sicher`
* Erschwert das Testen
* Verstößt gegen das Prinzip der `Einzelverantwortung`
    -> muss mehrere Dinge gleichzeitig tun (z.B. `Loggen` und Instanz verwalten)

Es nutzt einen `privaten Konstruktor`, der verhindert, dass man Objekte mit `new` erstellt. Wir müssen einen schreiben, weil sonst der `Default-Konstruktor` genutzt wird, der `public` ist.
Es gibt immer eine `statische Variable` (statisch, damit man sie nutzen kann, ohne ein Objekt der Klasse zu erstellen), die die `Instanz` speichert.
Der letzte Baustein ist eine `statische Methode` (z.B. `getInstance`), die die `Instanz` zurückgibt oder eine neue erstellt, falls keine existiert.

Beispiel:
```java
public class Logger
{
    // Statische Variable zum Speichern einer Instanz
    private static Logger instance;

    // Privater Konstruktor
    private Logger()
    {

    }

    // Methode zum Zurückgeben der Instanz
    public static Logger getInstance()
    {
        // Wenn es noch keine gibt, wird eine erstellt
        if (instance == null)
        {
            instance = new Logger();
        }
        return instance;
    }

    // Weitere Methode des Loggers
    public void log(String message)
    {
        System.out.println("[LOG] " + message);
    }
}
```

---

## Builder

Der `Builder` sorgt dafür, dass `komplexe Objekte` einfacher erstellt werden können.
Der Builder ist ein `Creational Design Pattern` und löst das Problem, dass ein `Konstruktor` zu kompliziert wird.
Außerdem kann man mit einem Builder unterschiedliche Varianten eines Objekts erstellen.

<br>

**Vorteile:**
* Gute Lesbarkeit und Verständlichkeit des Codes
* Kein verwirrender Konstruktor
* Flexibel, durch Kombination verschiedener Parameter
* Unveränderliches Objekt, nachdem es mit `build()` gebaut wurde

**Nachteile:**
* Viel Codeaufwand
* Bei einfachen Objekten unnötig / zu komplex
* Funktioniert nicht gut, wenn man nicht weiß, wie das finale Objekt aussehen soll

Was macht der `Builder` anders als eine `Abstract Factory`?
Der Builder erzeugt ein einzelnes Objekt Schritt für Schritt, während eine Abstract Factory fertige Objekte verschiedener Produktfamilien erstellt.

Beispiel:
```java
new Sandwich("Weißbrot", true, true, false, true, false, true);
```
Man weiß nicht mehr, welcher Parameter was macht und was er bestimmt.
Um dieses Problem zu lösen, schreibt man einen `Builder`.

Ein Builder nutzt sogenanntes `Method Chaining`.

### Method Chaining

Beispiel für Method Chaining:
```java
// Hier ist es ohne Method Chaining
// Das Objekt muss immer neu aufgerufen werden
Sandwich sandwich = new Sandwich();
sandwich.setBread("Weißbrot");
sandwich.withCheese(true);


// Hier mit Method Chaining
Sandwich sandwich = new Sandwich()
    .setBread("Weißbrot")
    .withCheese(true)
    .build();
```
Damit das funktioniert, muss die Methode das aktuelle Objekt zurückgeben.
```java
public Builder withCheese(boolean cheese)
{
    this.cheese = cheese;
    return this;
}
```

Umsetzung:
```java
// Hier ist die Sandwich-Klasse ohne einen Builder
public class Sandwich
{
    private String bread;
    private boolean cheese;

    public Sandwich(String bread, boolean cheese)
    {
        this.bread = bread;
        this.cheese = cheese;
    }
}
```
Jetzt machen wir aus der Klasse eine Klasse mit einem Builder, der uns die Sandwiches baut.

```java
public class Sandwich
{
    // Finale Attribute
    private final String bread;
    private final boolean cheese;

    // Privater Konstruktor, der nur Builder-Objekte akzeptiert
    private Sandwich(Builder builder)
    {
        this.bread = builder.bread;
        this.cheese = builder.cheese;
    }

    // In das gleiche File kommt eine neue Klasse namens Builder
    public static class Builder
    {
        // Nicht finale Attribute
        private String bread;
        private boolean cheese;

        // Um eine Ausfüllung von Feldern zu erzwingen,
        // schreibt man sie in den Builder-Konstruktor

        // Das ermöglicht z.B., dass jedes Sandwich mindestens Brot haben muss
        public Builder(String bread)
        {
            this.bread = bread;
        }

        // Alle weiteren, nicht zwingenden Attribute werden mithilfe von Methoden festgelegt
        public Builder withCheese(boolean cheese)
        {
            this.cheese = cheese;
            return this;
        }
        // Rückgabewert ist ein Builder -> für Method Chaining

        // Das Wichtigste ist die build()-Methode
        // Diese sorgt dafür, dass das finale Objekt zurückgegeben wird
        public Sandwich build()
        {
            return new Sandwich(this);
        }
    }
}
```

Da diese Klasse nicht wirklich lang ist, braucht man hier eher nicht zwingend einen Builder.
<br>

---

## Abstract Factory

Die `Abstract Factory` ist ebenfalls ein `Creational Design Pattern`.
Diese ermöglicht es, `zusammengehörige Objekte einer bestimmten Familie` zu erstellen, ohne deren konkrete Klassen anzugeben.
Die Erstellung erfolgt über eine abstrakte Fabrik, die je nach gewählter Variante unterschiedliche konkrete Objekte liefert.

Welches Problem dieses Pattern löst:

Wenn man ein Programm hat, das mit 2 Produkten arbeitet:

Es gibt einmal die `GPU` bzw. Grafikkarten.
Diese hat `Asus`-Karten und `MSI`-Karten.

Dann gibt es noch den `Monitor`.
Diese hat `Asus`-Monitore und `MSI`-Monitore.

Um nicht immer mit einer `if`-Abfrage prüfen zu müssen, ob man eine GPU oder einen Monitor haben will, benutzt man eine `Abstract Factory`.
Mithilfe von dieser kann man es deutlich einfacher darstellen und mit weniger Code.

**Vorteile:**
* Klare Trennung der Produktfamilien
* Anwendungscode bleibt unabhängig von den konkreten Klassen
* Einfache Erweiterung
* Einheitliche Schnittstelle

**Nachteile:**
* Mehr Codeaufwand durch Klassen und Interfaces
* Unflexibel, wenn Produkte gemischt werden sollen
* Überdimensioniert / zu komplex für einfache Strukturen

Beispiel:

Wir wollen GPUs und Monitore produzieren.
Es gibt Asus- und MSI-Monitore und -GPUs.

So schaut unsere Ordnerstruktur aus:
```
- java/
    - factory/
        - AbstractFactory.java // Interface
        - AsusFactory.java
        - MsiFactory.java
    - product/
        - interfaces/
            - Monitor.java     // Interface
            - GPU.java         // Interface
        - concrete/
            - AsusMonitor.java
            - MsiMonitor.java
            - AsusGPU.java
            - MsiGPU.java
    Main.java
```

Kommen wir zum Inhalt der einzelnen Klassen und was sie tun:

Fangen wir beim `product/`-Ordner an, `interfaces`:
```java
public interface Monitor
{
    String assemble();
}
```
```java
public interface GPU
{
    String assemble();
}
```
Mit diesen Interfaces wird festgelegt, dass jeder `Monitor` und jede `GPU` eine `assemble`-Methode braucht.
<br>

### Was bedeutet Concrete?

Eine konkrete (`concrete`) Klasse ist ein fertiges Bauteil (z.B. der MsiMonitor), das man sofort benutzen kann (`new MsiMonitor()`), weil es alle seine Aufgaben (`assemble()`) bereits umgesetzt hat.

Kommen wir jetzt zum Ordner `concrete`:
```java
public class AsusMonitor implements Monitor
{
    @Override
    public String assemble()
    {
        return "Asus Monitor zusammengebaut";
    }
}
```
```java
public class MsiMonitor implements Monitor
{
    @Override
    public String assemble()
    {
        return "MSI Monitor zusammengebaut";
    }
}
```
```java
public class AsusGPU implements GPU
{
    @Override
    public String assemble()
    {
        return "Asus GPU zusammengebaut";
    }
}
```
```java
public class MsiGPU implements GPU
{
    @Override
    public String assemble()
    {
        return "MSI GPU zusammengebaut";
    }
}
```
Diese `concrete`-Klassen legen fest, wie ein Monitor oder eine GPU zusammengebaut werden soll.
<br>

Kommen wir jetzt zum letzten Ordner, `factory`:
Hier gibt es drei Klassen.

`AbstractFactory.java`
Diese Klasse legt fest, welche Methoden benötigt werden, um eine allgemeine `GPU` oder einen allgemeinen `Monitor` zu erstellen.
Also ohne dass diese `Factory` weiß, ob es `Asus` oder `MSI` wird.
```java
public interface AbstractFactory
{
    public GPU createGPU();
    public Monitor createMonitor();
}
```
Jetzt gibt es noch die beiden Klassen, die dieses `Interface` verwenden.
Diese legen jetzt fest, ob es eine `MSI GPU/Monitor` oder `Asus GPU/Monitor` wird.
```java
public class AsusFactory implements AbstractFactory
{
    @Override
    public GPU createGPU()
    {
        return new AsusGPU();
    }

    @Override
    public Monitor createMonitor()
    {
        return new AsusMonitor();
    }
}
```
```java
public class MSIFactory implements AbstractFactory
{
    @Override
    public GPU createGPU()
    {
        return new MSIGPU();
    }

    @Override
    public Monitor createMonitor()
    {
        return new MSIMonitor();
    }
}
```
Jetzt haben wir das geschafft.
Als Letztes brauchen wir noch die `Main`-Klasse:
```java
public class Main
{
    public static void main(String[] args)
    {
        AbstractFactory msi = new MSIFactory();
        GPU msiGPU = msi.createGPU();
        Monitor msiMonitor = msi.createMonitor();

        AbstractFactory asus = new AsusFactory();
        GPU asusGPU = asus.createGPU();
        Monitor asusMonitor = asus.createMonitor();
    }
}
```
Jetzt haben wir das `Abstract Factory Pattern` angewendet.
<br>
