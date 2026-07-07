# Collections

## Inhaltsverzeichnis
* [Methoden](#methoden)
* [Compare](#compare)
* [For-Each-Schleife](#for-each-schleife)
* [Verschiedene Collections](#verschiedene-collections)
    * [Array List](#array-list)
    * [TreeSet](#treeset)
    * [HashSet](#hashset)
    * [LinkedList](#linkedlist)
    * [Maps](#maps)

---

Collections haben Vorteile gegenüber Arrays. Collections können wachsen (Arrays haben einen fixen Index).
Alle diese Methoden haben `Rückgabewerte`!
<br>

## Methoden
```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<String>(5);
        list.add("A");
        list.add("B");
        list.add("C");
        list.add("D");

        // Druckt die gesamte Liste
        System.out.println("--- List ---");
        System.out.println(list);

        // Fügt ein Element der Liste hinzu
        System.out.println("--- Add ---");
        list.add("E");
        System.out.println(list);

        // Entfernt ein Element (nach Index oder Element)
        System.out.println("--- Remove ---");
        list.remove("B");
        System.out.println(list);

        // Gibt ein Objekt aufgrund des Index zurück
        System.out.println("--- Get ---");
        System.out.println(list.get(0));

        // Gibt den Index aufgrund eines Objektes zurück
        System.out.println("--- Index Of ---");
        System.out.println(list.indexOf("D"));

        // Die Länge / Größe
        System.out.println("--- Size ---");
        System.out.println(list.size());

        // Ob die Collection leer ist
        System.out.println("--- is Empty ---");
        System.out.println(list.isEmpty());

        // Aus der Collection ein Array machen
        System.out.println("--- To Array ---");
        System.out.println(list.toArray());
    }
}
```
<br>

## Compare
Die Compare-Methode benutzt man, um Objekte zu sortieren oder zu vergleichen. Wenn die verglichenen Objekte gleich sind, ist das Ergebnis 0, wenn eines kleiner ist -1, und größer 1 usw. Es kommt zurück, wie weit die Objekte voneinander entfernt sind. Bei Strings ist A zu Z weiter weg als A zu B. `compareTo` bei Objekt-Datentypen, `compare` bei primitiven Datentypen.

Es gibt die `compare`- und die `compareTo`-Methode. Bei `compare` werden zwei Dinge verglichen:
```java
package at.htlle.reiti.oopuebungen.buecher4;

import java.util.Comparator;

public class CompByYear implements Comparator<Item>
{
    @Override
    public int compare(Item o1, Item o2)
    {
        return Integer.compare(o1.getYear(), o2.getYear());
    }
}
```

`implements` implementiert bestimmte Interfaces.
Um die `Compare`-Methode zu implementieren, schreibt man:
```java
public class ClassName implements Comparable<ClassName>
```
Man muss die Methode `compareTo(ClassName object)` überschreiben.
Um zwei `Strings` zu vergleichen, schreibt man die `compareTo`-Methode so:
```java
@Override
public int compareTo(ClassName o)
{
    return this.name.compareTo(o.name);
}
```
Um ein Array nach bestimmten Kriterien zu sortieren, brauchen wir:
```java
Arrays.sort(arrayName);
```
Um eine Collection zu sortieren, schreiben wir:
```java
Collections.sort(arrayList);
```
<br>

## For-Each-Schleife
Der String `s` bekommt beim ersten Durchlauf den ersten Wert der Liste und druckt ihn aus.
```java
for (String s : list)
{
    System.out.println(s);
}
```

---

# Verschiedene Collections

## Array List
Ist eine Array-Liste, die das Speichern von Elementen in einer geordneten Reihenfolge zulässt. `Duplikate` sind erlaubt! Man kann über den `Index` auf Elemente zugreifen. Es gibt auch keine fixe Größe, sie ändert sich je nach Bedarf. Man kann bei einer Liste mit einem Index auf die einzelnen Objekte zugreifen.

```java
List<String> arrayList = new ArrayList<>();
arrayList.add("A");
arrayList.add("B");
arrayList.add("A"); // Duplikate sind erlaubt
```
<br>

## TreeSet
Implementiert das `Set`-Interface und speichert Elemente in Reihenfolge. Es ist auf einer Art Baum aufgebaut. Es sind keine `Duplikate` erlaubt! Ein Set hat keinen Index. Also geht es nicht mit einer normalen For-Schleife. Es wird immer so sortiert:
```
        7
      /   \
    5       14
   / \      / \
```

## HashSet / LinkedList
*(Hinweis: Inhalt hier ergänzen, war in der Originaldatei nicht vollständig ausformuliert.)*

<br>

## Maps
Sind immer `Key-Value`-Paare. Jeder Key ist einzigartig und muss eindeutig sein. Die Values können auch gleich sein. Bei den Values kann jeder Datentyp vorkommen. Ein Key weist immer genau auf einen Wert hin. Keys sind eine Art Index, den wir selbst wählen können.

```java
KEY => int
VALUE => String
```
Wir können eine Map mit `System.out.println(mapName)` einfach mit Key und Value ausgeben. Eine Map wird so erstellt:
```java
Map<Integer, String> map = new HashMap<Integer, String>();

map.put(1, "Schieder");
map.put(2, "Trafella");
map.put(3, "Winter");
map.put(4, "Rezaie");
map.put(5, "Störenfried");

System.out.println(map);
```
