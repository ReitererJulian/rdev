# Structural Design Patterns

## Inhaltsverzeichnis
* [Adapter](#adapter)
* [Proxy](#proxy)
* [Facade](#facade)

---

Structural Design Patterns sind `Design Patterns`, die sich mit der Zusammensetzung von Klassen und Objekten beschäftigen.

Die drei wichtigsten sind:
* `Adapter`
* `Proxy`
* `Facade`

---

## Adapter

Der `Adapter` ist ein `Structural Design Pattern`.
Dieses ermöglicht es, dass ein bereits bestehendes System mit inkompatiblen Schnittstellen zusammenarbeitet.
Einen `Adapter` zu benutzen macht Sinn, wenn man die Klasse, die man benutzen will, nicht ändern kann.
    -> z.B. eine Klasse aus einer `externen Bibliothek`

<br>

**Vorteile:**
* Integration von alten oder inkompatiblen Klassen
* Kein Eingriff in bestehende oder fremde Klassen notwendig
* Klare Trennung zwischen System und Fremdkomponente
* Einhaltung des Open/Closed-Prinzips
    -> offen für Erweiterungen, geschlossen für Änderungen

**Nachteile:**
* Zusätzlicher Klassen- und Wartungsaufwand
* Kann zu Overhead führen, bei zu vielen Adaptern
* Gefahr von Performanceverlust bei zu komplexen Umrechnungen in Adapterklassen

<br>

**Unterschied Adapter zu Facade:**

Ein `Adapter` passt eine einzelne Klasse an die neue Schnittstelle an.
Eine `Facade` bietet eine vereinfachte Schnittstelle zu einem ganzen `Subsystem`.

<br>

Das einfachste Beispiel ist ein Netzteil, z.B. für ein iPhone.
Man kann das Kabel des iPhones nicht direkt in die Steckdose stecken.
Das geht nur mit einem Netzteil/Adapter, welches den USB-C-Eingang mit der Buchse kompatibel macht.

```
| USB-C  | <--- | Netzteil | <--- | Steckdose |

| Target | <--- | Adapter  | <--- | Adaptee   |
```

<br>

Ordnerstruktur:
```
- java/
    - main/
        - Main.java
    - adapter/
        - USBC_Power_In.java  // Target-Interface
        - PowerAdapter.java   // Der Adapter
    - legacy/
        - WallSocket.java     // Das Adaptee (die inkompatible Klasse)
```

Code:
```java
// Target (was das Gerät braucht)
public interface USBC_Power_In
{
    String getPowerToDevice();
}
```

Dafür müssen wir den Adapter schreiben, um das USB-C zu verbinden:
```java
// Adaptee (die Quelle, die angepasst werden muss)
public class WallSocket
{
    public String getPowerFromSocket()
    {
        return "Power";
    }
}
```

Um diese zwei Klassen zu verbinden, müssen wir eine neue Adapterklasse schreiben.
Diese muss das `USBC`-Interface implementieren und einen `WallSocket` anlegen.
```java
public class PowerAdapter implements USBC_Power_In
{
    // Ist final, damit immer nur auf ein WallSocket-Objekt gezeigt wird
    private final WallSocket wallSocket;

    // Konstruktor, um das genaue WallSocket-Objekt mitzugeben
    public PowerAdapter(WallSocket wallSocket)
    {
        this.wallSocket = wallSocket;
    }

    // Methode aus dem Interface implementieren
    @Override
    public String getPowerToDevice()
    {
        return wallSocket.getPowerFromSocket();
    }
}
```
<br>

Anwendung in der `Main`-Klasse:
```java
public class Main
{
    public static void main(String[] args)
    {
        // Inkompatible Quelle
        WallSocket socket = new WallSocket();

        // Adapter erstellen, der die Quelle transformiert
        USBC_Power_In adapter = new PowerAdapter(socket);

        // Über den Adapter wird getPowerFromSocket() aufgerufen
        adapter.getPowerToDevice();
    }
}
```
<br>

---

## Proxy

`Proxy` heißt übersetzt Stellvertreter.
Ein `Proxy` stellt also einen Stellvertreter für ein Objekt bereit.
Mit dem `Proxy Pattern` ist es dadurch möglich, den Zugriff auf Objekte zu `kontrollieren`, zu `verzögern` oder zu `erweitern`.
Das alles passiert, ohne das `Originalobjekt` zu verändern.

<br>

**Vorteile:**
* Ermöglicht kontrollierten Zugriff auf das Originalobjekt
* Unterstützt Lazy Loading
* Ermöglicht Sicherheitsprüfungen wie Logging
* Kann externe Abhängigkeiten abschirmen

**Nachteile:**
* Zusätzlicher Codeaufwand
* Bei übermäßigem Einsatz wird es schnell zu komplex
* Bei falscher Implementierung ist der Proxy eventuell nicht transparent
    -> könnte zu unerwartetem Verhalten führen

<br>

**Anwendungsbeispiele:**
* `Schutzproxy` -> prüft Zugriffsrechte
* `Remote Proxy` -> Objekte über Netzwerk steuern
* `Virtual Proxy` -> Objekte mit Lazy Loading verzögert erstellen lassen
* `Logging`, `Caching`, `Überwachung`

<br>

**Vergleich mit Adapter:**
Ein Adapter macht eine inkompatible Schnittstelle kompatibel.
Ein Proxy steuert oder erweitert den Zugriff auf ein Objekt, das bereits kompatibel ist.

<br>

Beispiele:
* wenn ein Objekt vor Zugriff geschützt werden muss
* wenn bei jeder Erstellung geloggt wird

Hier ist das Beispiel mit Logging in Code:

Ordnerstruktur:
```
- java
    - proxy
        - LoggingProxy.java   // Erweiterung des RealService (mit Logging)
    - service
        - Service.java
        - RealService.java    // Klasse, zu der wir einen Proxy schreiben
    - Main.java
```

```java
public interface Service
{
    void request();
}
```
```java
public class RealService implements Service
{
    @Override
    public void request()
    {
        System.out.println("Anfrage wird verarbeitet");
    }
}
```
Jetzt schreiben wir den Proxy, der jedes Mal bei einer Anfrage (`request()`) an den `Service` eine Meldung loggt.
```java
public class LoggingProxy implements Service
{
    private final RealService realService;

    public LoggingProxy(RealService realService)
    {
        this.realService = realService;
    }

    @Override
    public void request()
    {
        System.out.println("[LOG] Zugriff auf Service");
        realService.request();
    }
}
```
Hier ist noch die `Main`-Klasse:
```java
public class Main
{
    public static void main(String[] args)
    {
        Service proxy = new LoggingProxy(new RealService());

        // Wird zuerst über den Logging-Proxy umgeleitet
        // Schreibt zuerst [LOG]... dann wird realService.request() ausgeführt
        proxy.request();
    }
}
```
<br>

---

## Facade

Ist auch ein `Structural Design Pattern`.
Es bietet eine `vereinfachte Schnittstelle` zu einem komplexen `Subsystem` und verdeckt dabei dessen Details und Komplexität.

Ist sinnvoll, wenn man nicht mit jedem `Subsystem` einzeln interagieren will.

**Beispiel:**
* Audio -> turnOn()
* Video -> playMovie()
* TV -> turnOn()

Hier müsste man alle einzeln aufrufen:
```java
Audio audio = new Audio();
Video video = new Video();
Tv tv = new Tv();

audio.turnOn();
video.playMovie();
tv.turnOn();
```
Mit einer `Facade` fasst man alle diese Methoden in einer neuen zusammen, damit es einfacher und übersichtlicher wird.

<br>

**Vorteile:**
* Einfache Verwendung komplexer Systeme
* Trennung zwischen Schnittstelle und Implementierungsdetails
* Weniger Kopplung zwischen Benutzer und Subsystem
* Lesbarerer und wartbarer Code auf Seiten des Clients

**Nachteile:**
* Kann zum `God Object` werden
    -> durch zu viele Funktionen
* Versteckt Funktionen vor fortgeschrittenen Benutzern
* Kann dazu führen, dass neue Anforderungen wieder zur internen Struktur durchbrechen müssen

**Vergleich mit Adapter:**
Ein Adapter macht eine inkompatible Schnittstelle kompatibel.
Eine Facade bietet eine neue, vereinfachte Schnittstelle für das ganze System.

<br>

Einfaches Beispiel:

Ein Benutzer möchte einen Computer starten, er will nicht jede Komponente einzeln initialisieren.

Der Computer besteht aus `CPU`, `RAM` und `Storage`.

Die `Facade` kümmert sich intern darum, dass alle Subsysteme in der richtigen Reihenfolge aufgerufen werden.

Ordnerstruktur:
```
- java
    - facade
        - ComputerFacade.java
    - subsystems
        - CPU.java
        - RAM.java
        - Storage.java
    - Main.java
```

<br>

`CPU.java`:
```java
public class CPU
{
    public void start()
    {
        System.out.println("System is starting");
    }
}
```
`RAM.java`:
```java
public class RAM
{
    public void loadOS()
    {
        System.out.println("OS is loading");
    }
}
```
`Storage.java`:
```java
public class Storage
{
    public void readBoot()
    {
        System.out.println("Reading boot sector");
    }
}
```
Jetzt verbinden wir diese Klassen in einer neuen Klasse, in der die Methoden zusammen aufgerufen werden.

`ComputerFacade.java`:
```java
public class ComputerFacade
{
    private final CPU cpu = new CPU();
    private final RAM ram = new RAM();
    private final Storage storage = new Storage();

    public void turnOn()
    {
        cpu.start();
        ram.loadOS();
        storage.readBoot();
    }
}
```
<br>

Jetzt kommt wie immer die Anwendung in der `Main`-Klasse:
```java
public class Main {
    public static void main(String[] args) {

        ComputerFacade computer = new ComputerFacade();

        computer.turnOn();
    }
}
```
