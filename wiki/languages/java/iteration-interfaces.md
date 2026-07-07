# Anonyme Klassen, Iteratoren, Interfaces

## Inhaltsverzeichnis
* [Anonyme Klasse](#anonyme-klasse)
* [Iteratoren / Iteration](#iteratoren--iteration)
* [Interfaces](#interfaces)

---

## Anonyme Klasse

Eine anonyme Klasse ist in diesem Fall eine Unterklasse von `DirtyCar`. Anonyme Klassen sind eine Art von Unterklassen, in denen man Methoden überschreiben, hinzufügen, neue Attribute hinzufügen usw. kann.

```java
Car car1 = new DirtyCar("Name", "Farbe")
{
    @Override
    public int compareTo(Car c)
    {
        return this.getName().compareTo(c.getName());
    }
};
```

---

## Iteratoren / Iteration

Iteration bedeutet, dass es immer um eins mehr wird. Wenn wir ein Array / eine Collection durchlaufen, schreiben wir:
```java
for (int i = 0; i < arrayName.length(); i++)
// Während i kleiner als die Array-Länge ist, wird i immer um eins erhöht. Das ist der Iterator.
```

Wenn man eine Collection durchläuft und dabei ändern will, benötigen wir einen Iterator. Wenn wir sie nur durchlaufen wollen, benutzen wir eine For-Schleife.

Um einen Iterator zu coden, müssen wir `java.util` importieren. Man schreibt ihn so:
```java
Iterator<String> iter = field.iterator();
// Wir haben eine Collection mit Datentyp String.
// Wir bekommen den Iterator über unsere Collection "field".
```
Um jetzt ein Element zu löschen, brauchen wir einen Iterator. Hier ist ein Beispiel:
```java
package at.htlle.reiti.collections.iterations;

import java.util.*;

public class TestingMain
{
    public static void main(String[] args)
    {
        // hier wird ein neues String-HashSet erstellt
        Set<String> field = new HashSet<String>();

        field.add("Trafella");
        field.add("Ranninger");
        field.add("Rezaie");
        field.add("Winter");
        field.add("Störenfried");

        // hier wird ein Iterator erstellt (Datentyp String)
        Iterator<String> iter = field.iterator();

        // während es ein nächstes Element gibt
        while (iter.hasNext())
        {
            // speichert das aktuelle Element in einem String
            String string = iter.next();

            // gibt den String aus
            System.out.println(string);
            if (string.equals("Störenfried"))
            {
                // Das Element "Störenfried" wird gelöscht, indem wir auf das aktuelle Element zugreifen
                iter.remove();
            }
        }
        System.out.println(field.size());
    }
}
```

Wir benutzen Iteratoren, um Collections sicher zu modifizieren, da bei einer For-Loop eine `ConcurrentModificationException` geworfen wird.

---

## Interfaces

Gibt vor, welche Methoden implementiert werden müssen. Es kommen nur Methodenköpfe in ein Interface. Warum sollte man so etwas machen? Um einen Standard zu erfüllen. Zum Beispiel, wenn eine Klasse Methoden zum Fahren und Bremsen braucht. Wenn man will, dass eine Methode in allen Klassen vorhanden ist, ohne die Vererbung ändern zu müssen.

```java
// Definition des Interfaces
interface Fahrzeug {
    void fahren();
    void bremsen();
}
```
Hier wird nur das Interface mit den Methoden `fahren()` und `bremsen()` definiert. Jede Klasse, die dieses Interface implementiert, braucht diese beiden Methoden.

<br>

```java
// Implementierung des Interfaces in der Klasse Auto
class Auto implements Fahrzeug {
    @Override
    public void fahren() {
        System.out.println("Das Auto fährt.");
    }
    @Override
    public void bremsen() {
        System.out.println("Das Auto bremst.");
    }
}

// Implementierung des Interfaces in der Klasse Fahrrad
class Fahrrad implements Fahrzeug {
    @Override
    public void fahren() {
        System.out.println("Das Fahrrad fährt.");
    }
    @Override
    public void bremsen() {
        System.out.println("Das Fahrrad bremst.");
    }
}
```
<br>
