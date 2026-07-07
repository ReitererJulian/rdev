# @Override: equals, toString, hashCode

## Inhaltsverzeichnis
* [Equals Methode](#equals-methode)
* [To String](#to-string)
* [Hash Code](#hash-code)

---

## Equals Methode

Hier ist ein Beispiel für eine `equals`-Methode.
```java
@Override
public boolean equals(Object obj)
{
    if (this == obj)
    {
        return true;
    }

    if (obj == null || this.getClass() != obj.getClass())
    {
        return false;
    }

    CCar other = (CCar) obj;

    if (this.getName().equals(other.getName())
    && this.getColor().equals(other.getColor())
    && this.fuelCapacity == other.fuelCapacity)
    {
        return true;
    }
    else
        return false;
}
```

### Schritt-für-Schritt-Erklärung

**Erster Teil**
Da es schon eine `.equals()`-Methode gibt, müssen wir die jetzige überschreiben.
Die Methode muss gleich heißen.
Danach legen wir die Methode an, die einen `Object`-Datentyp akzeptiert.
Im ersten `if`-Statement fragen wir, ob `this` das Objekt ist, das hineingegeben wird.
Wenn ja, dann `return true`.
<br>

**Zweiter Teil**
Im nächsten Schritt wird geprüft, ob das `obj` `null` ist.
Wenn es `null` ist, können wir nicht mit einem `.` arbeiten. Sonst kommt eine `NullPointerException`.
Danach wird geprüft, ob die zwei Objekte (`this` und `obj`) aus der gleichen Klasse kommen.
Wenn sie nicht aus der gleichen Klasse kommen, wird `false` zurückgegeben.
Wir können ja nicht `Autos` und `Fahrräder` vergleichen.
<br>

**Datentypumwandlung**
`CCar other = (CCar) obj;` wird verwendet, um das mitgegebene `obj` in ein `CCar` mit dem Namen `other` umzuwandeln.
Das müssen wir machen, damit wir später zwei `CCar`-Autos vergleichen können.
Man muss das auch machen, damit man auf die `Attribute` zugreifen kann.
<br>

**Dritter Teil**
Diese große `if`-Verzweigung ist der letzte Teil der `equals`-Methode.
`if (this.getName().equals(other.getName())` – hier wird der Name von `this` und `other` verglichen.
`&& this.getColor().equals(other.getColor())`
`&& this.fuelCapacity == other.fuelCapacity)`
In diesen zwei letzten Abfragen werden die Farbe (`color`) und die `fuelCapacity` verglichen.
Wenn alles gleich ist, wird `true` zurückgegeben, sonst `false`.
<br>

---

## To String

Eine `toString`-Methode wird verwendet, um eine benutzerdefinierte `String`-Darstellung eines Objekts zu erzeugen.
Die Standard-`toString`-Methode ist in der `Object`-Klasse definiert.

**Beispiel**:

`Superklasse`:
```java
@Override
public String toString()
{
    return name + " " + color + " Speed: " + speed;
}
```
`Unterklasse`:
```java
@Override
public String toString()
{
    // super.toString() = name, color und speed aus der Superklasse
    return super.toString() + " Battery: " + batteryCapacity;
}
```
So sieht die Ausgabe aus: `Tesla weiß Speed: 0 Battery: 57.5`
Name, Color und Speed kommen aus der Superklasse, batteryCapacity aus der Unterklasse.

---

## Hash Code

Gibt einen `Integer` (Ganzzahl) zurück. Der Hashcode bestimmt den Ort eines Objekts genauer.
Wenn in einer Klasse zwei Objekte existieren, die laut der `equals`-Methode gleich sind, ist auch der Hashcode gleich.
Die Parameter, die wir mitgeben, sind dieselben, die wir auch in der `equals`-Methode vergleichen.

**Beispiel**
```java
// Hash-Methode
@Override
public int hashCode()
{
    return Objects.hash(name);
}
```

### Methoden

Methoden, die ich für die PLÜ benötige, um Items `hinzuzufügen`, zu `entfernen` oder `auszugeben`.
Beispiel aus der Restaurant-Übung, in der Reihenfolge:

`Item hinzufügen`
```java
public boolean addMenuItem(MenuItem item)
{
    if (counter >= Constants.MAX_ORDER)
    {
        return false;
    }
    else
    {
        savedMenu[counter] = item;
        counter++;
        return true;
    }
}
```

`Item entfernen`
```java
public boolean removeMenuItem(MenuItem item)
{
    for (int i = 0; i < counter; i++)
    {
        if (savedMenu[i] != null && savedMenu[i].equals(item))
        {
            savedMenu[i] = savedMenu[counter - 1];
            savedMenu[counter - 1] = null;
            counter--;
            return true;
        }
    }
    return false;
}
```

`Array drucken`
```java
public void printMenu()
{
    for (int i = 0; i < counter; i++)
    {
        System.out.println(savedMenu[i].getDetails());
    }
}
```
<br>
