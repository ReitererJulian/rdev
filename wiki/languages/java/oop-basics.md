# Java OOP Basics

## Inhaltsverzeichnis
* [Klasse](#klasse)
* [Objekt](#objekt)
* [Unterschied `--var` und `var--`](#unterschied---var-und-var--)
* [Instanz](#instanz)
* [abstract](#abstract)
* [static](#static)
* [Attribute](#attribute)
* [Datenkapselung](#datenkapselung)
* [this](#this)
* [Konstruktoren](#konstruktoren)
* [super](#super)
* [Vererbung](#vererbung)
* [Abstraktion](#abstraktion)
* [Polymorphismus](#polymorphismus)

---

## Klasse
Ist ein Keksausstecher / eine Schablone.
`Klassen` erben von der `Object`-Klasse.
Hat `Attribute`, beim Auto z.B. die Farbe.
Man kann `Methoden` (`Getter` und `Setter`) und `Konstruktoren` verwenden und weitergeben.

<br>

## Objekt
**Das Objekt ist die Instanz einer Klasse.**
Eine Identität, die aus einer Klasse erstellt wird.
Hat Attribute aus der Klasse, aus der es erstellt worden ist.
```java
Car myCar = new Car();
myCar.setColor("blue");
```
<br>

## Unterschied `--var` und `var--`
Wenn vor der Variable `--` steht, wird die Variable zuerst um 1 verringert und dann verwendet.
Wenn nach der Variable `--` steht, wird die Variable zuerst benutzt und dann um 1 verringert.
```java
int a = 5;
int b = --a; // a wird auf 4 verringert, und dann wird b der Wert 4 zugewiesen

int x = 5;
int y = x--; // y wird der Wert 5 zugewiesen, und dann wird x auf 4 verringert
```

## Instanz
Ein konkretes Objekt aus einer Klasse.
Ein Beispiel: Die Klasse Auto hat als Eigenschaft die Farbe und eine Methode `fahren`. Wenn man aus dieser
Klasse drei Objekte erstellt, hat jedes eine eigene Farbe, und alle können fahren (Verhalten). Die drei sind
dann drei Instanzen dieser Klasse.
<br>

## abstract
Eine `abstract` Klasse kann man nicht `instanziieren`.
Sie dient nur als Vorlage für andere `Unterklassen`.
```java
public abstract class Car
```
Die Car-Klasse ist jetzt `abstract`.

<br>

## static
Benutzt man, wenn man kein Objekt und keine Instanz einer Klasse braucht,
z.B. bei `Konstanten`.
```java
public class Constants
{
     public final static int MAX_AUTOS = 5;
}
```
`final` sorgt dafür, dass die Variable nicht mehr veränderbar ist.
<br>

## Attribute
Werden auch `Eigenschaften` genannt.
Werden in Klassen angelegt, um diese `Variablen` in `Objekten` zu benutzen.
```java
public class Car
{
    public String color;
}
```
<br>

## Datenkapselung
Wird verwendet, damit `Variablen` nur über `Methoden` geändert werden können.
Indem man die Variablen `private` setzt, kann man nur mehr innerhalb der Klasse darauf zugreifen.
```java
public class Car
{
    private String color;

    public String getColor()
    {
        return color;
    }

    public void setColor(String color)
    {
        this.color = color;
    }
}
```
Die Variable `color` kann man nur mehr so aufrufen / bearbeiten:
```java
{
    Car myCar = new Car();
    myCar.setColor("blue");
}
```
Das passiert in einer anderen Klasse.
<br>

## this
Der Operator `this` weist auf das aktuelle `Objekt` hin.
`this` wird meist in `Konstruktoren` verwendet.
In Konstruktoren weist man mit `this` auf die `Instanzvariable` hin. Die `Instanzvariable` ist eine Variable, die außerhalb der Methode deklariert wurde.

```java
public class Car
{
    //Instanzvariable
    private String color;

    public Car(String color)
    {
        this.color = color;
        // Die Instanzvariable ist das, was im Konstruktor übergeben wird
    }
}
```
<br>

## Konstruktoren
`Konstruktoren` sind spezielle `Methoden`, die zur Initialisierung von Objekten verwendet werden.
Sie haben immer den Namen der Klasse und keinen Rückgabewert.
Wenn man keinen schreibt, macht der Compiler einen eigenen, ohne Parameter. Dieser heißt `Default Constructor`.

`Car`-Klasse:
```java
public class Car
{
    private String color;
    private int speed;

    //constructor
    public Car(String color, int speed)
        {
            this.color = color;
            this.speed = speed;
        }
}
```
`Main`-Klasse:
```java
public class Main
{
    public static void main(String[] args)
    {
        Car myCar = new Car("blue", 230);
    }
}
```
<br>

## super
`super` greift auf den Konstruktor der Ober-/Superklasse zu.
Mit `super("Datentyp variablenname")` kann man den passenden Konstruktor der `Superklasse` auswählen, je nachdem wie viele Argumente man hat.
<br>

## Vererbung
Beschreibt, wie `Attribute` von der obersten Klasse (`Superklasse`) in untere Klassen mitgenommen werden.
Man kann solche Oberklassen auch `abstract` machen, um sie nicht mehr `instanziieren` zu können.

`Superklasse`:
```java
public class Car // public abstract class Car
{
    private String color;
    private int speed;

    public Car(String color, int speed)
    {
        this.color = color;
        this.speed = speed;
    }
}
```
`Unterklasse`:
```java
public class ElectroCar extends Car
{
    private int price;

    public ElectroCar(String color, int speed, int price)
    {
        // ruft den Konstruktor mit den Parametern color und speed auf
        super(color, speed);
        this.price = price;
    }
}
```
<br>

## Abstraktion
Nur die relevanten Daten einbeziehen.
Für ein Autounternehmen wird z.B. die Augenfarbe des Fahrers `nicht` wichtig sein.
<br>

## Polymorphismus
Heißt auf Deutsch Vielgestaltigkeit.
Wenn man eine Methode hat, die gleich heißt, sich aber unterschiedlich verhält.
Z.B. bei `toString` oder `equals`. Die `equals`-Methode aus der Superklasse vergleicht standardmäßig nur die Speicheradressen.
<br>
