# Behavioral Design Patterns

## Inhaltsverzeichnis
* [Observer](#observer)
* [Strategy](#strategy)
* [State](#state)
* [Visitor](#visitor)

---

`Behavioral Patterns` befassen sich mit der Kommunikation zwischen Objekten.
Also wie Objekte miteinander kommunizieren.

---

## Observer

Erstellt eine 1:n-Beziehung zwischen Objekten.
Wenn sich der Zustand eines Objekts ändert, werden alle `Observer` (Beobachter) benachrichtigt.

**Beispiel:**
Eine Wetterstation misst Wetterdaten.
Wenn sich etwas verändert, werden alle Displays und Logger informiert.

Ordnerstruktur:
```
- java
    - model
        - WeatherStation
        - Display
        - Logger
    - observer
        - Observer (Interface)
        - Subject (Interface)
    - Main.java
```

Observer-Interface:
```java
public interface Observer
{
    void update(int temperature);
}
```

Subject-Interface:
```java
public interface Subject
{
    void addObserver(Observer observer);
    void notifyObservers();
}
```

Die Implementierung der beiden Interfaces:
```java
public class WeatherStation implements Subject
{
    // Liste zum Speichern von Observern
    private List<Observer> observers = new ArrayList<>();
    private int temperature;

    // Setzt die Temperatur und benachrichtigt alle Observer, dass sich etwas geändert hat
    public void setTemperature(int temperature)
    {
        this.temperature = temperature;
        notifyObservers();
    }

    // Ruft für jeden Observer die update-Methode mit der aktuellen Temperatur auf
    @Override
    public void notifyObservers()
    {
        for (Observer o : observers)
        {
            o.update(temperature);
        }
    }

    @Override
    public void addObserver(Observer observer)
    {
        observers.add(observer);
    }
}
```
<br>

Display:
```java
public class Display implements Observer
{
    @Override
    public void update(int temp)
    {
        System.out.println("Displayed temp: " + temp);
    }
}
```

Logger:
```java
public class Logger implements Observer
{
    @Override
    public void update(int temp)
    {
        System.out.println("[LOG] temp: " + temp);
    }
}
```
<br>

Main:
```java
public class Main
{
    public static void main(String[] args)
    {
        WeatherStation ws = new WeatherStation();

        ws.addObserver(new Display());
        ws.addObserver(new Logger());

        ws.setTemperature(28);
        ws.setTemperature(30);
    }
}
```

---

## Strategy

Das Strategy Pattern bietet verschiedene "Werkzeuge" (Strategien) für die gleiche Aufgabe an,
die man jederzeit einfach austauschen kann, ohne dass der Rest des Programms merkt, welches Werkzeug gerade benutzt wird.

Beispiel: Verschiedene Bezahlmethoden (Bar, Karte, ApplePay).

**Ordnerstruktur:**
```
- java
    - model
        - CheckoutSystem
    - strategy
        - PaymentStrategy (Interface)
        - CashPayment
        - CardPayment
        - ApplePay
    - Main
```

PaymentStrategy (Interface):
```java
public interface PaymentStrategy
{
    void pay(int amount);
}
```
<br>

CheckoutSystem:
```java
public class CheckoutSystem
{
    private PaymentStrategy strategy;

    public void setPaymentStrategy(PaymentStrategy strategy)
    {
        this.strategy = strategy;
    }

    public void executePayment(int amount)
    {
        strategy.pay(amount);
    }
}
```
<br>

Cash:
```java
public class CashPayment implements PaymentStrategy
{
    @Override
    public void pay(int amount)
    {
        System.out.println(amount + " Payed with Cash");
    }
}
```
<br>

Card:
```java
public class CardPayment implements PaymentStrategy
{
    @Override
    public void pay(int amount)
    {
        System.out.println(amount + " Payed with Card");
    }
}
```
<br>

ApplePay:
```java
public class ApplePay implements PaymentStrategy
{
    @Override
    public void pay(int amount)
    {
        System.out.println(amount + " Payed with ApplePay");
    }
}
```
<br>

Main:
```java
public class Main
{
    public static void main(String[] args)
    {
        CheckoutSystem counter = new CheckoutSystem();

        // Kunde zahlt mit Karte
        counter.setPaymentStrategy(new CardPayment());
        counter.executePayment(50);

        // Nächster mit ApplePay
        counter.setPaymentStrategy(new ApplePay());
        counter.executePayment(24);
    }
}
```

---

## State

Das State Pattern sorgt dafür, dass ein Objekt sein Verhalten einfach austauscht,
indem es den aktuellen Zustand gegen einen anderen wechselt.

Beispiel: Ein CD-Player hat 3 Zustände:
* Wiedergabe läuft (`play()`)
* Pausiert (`paused()`)
* Gestoppt (`stopped()`)

Je nach Zustand reagiert er anders
(z.B. kann er nicht wieder abspielen, da bereits gespielt wird).

**Ordnerstruktur:**
```
- java
    - model
        - Player
    - state
        - PlayerState (Interface)
        - PlayingState
        - PausedState
        - StoppedState
    - Main.java
```
<br>

PlayerState-Interface:
```java
public interface PlayerState
{
    void play(Player player);
    void pause(Player player);
    void stop(Player player);
}
```
<br>

Player:
```java
public class Player
{
    private PlayerState state;

    public Player()
    {
        // Bei Erstellung ist der Player gestoppt
        this.state = new StoppedState();
    }

    public void setState(PlayerState state)
    {
        this.state = state;
    }

    public void play()
    {
        state.play(this);
    }

    public void pause()
    {
        state.pause(this);
    }

    public void stop()
    {
        state.stop(this);
    }
}
```
<br>

PlayingState:
```java
public class PlayingState implements PlayerState
{
    @Override
    public void play(Player player)
    {
        // Kann nicht abspielen, da es bereits spielt
        System.out.println("[Error] Already playing");
    }

    @Override
    public void pause(Player player)
    {
        System.out.println("Pause Music");
        player.setState(new PausedState());
    }

    @Override
    public void stop(Player player)
    {
        System.out.println("Stopped Music");
        player.setState(new StoppedState());
    }
}
```
<br>

PausedState:
```java
public class PausedState implements PlayerState
{
    @Override
    public void play(Player player)
    {
        System.out.println("Music playing");
        player.setState(new PlayingState());
    }

    @Override
    public void pause(Player player)
    {
        // Kann nicht pausieren, da bereits pausiert
        System.out.println("[Error] Already Paused Music");
    }

    @Override
    public void stop(Player player)
    {
        System.out.println("Stopped Music");
        player.setState(new StoppedState());
    }
}
```
<br>

StoppedState:
```java
public class StoppedState implements PlayerState
{
    @Override
    public void play(Player player)
    {
        System.out.println("Music playing");
        player.setState(new PlayingState());
    }

    @Override
    public void pause(Player player)
    {
        // Kann nicht pausieren, da bereits gestoppt
        System.out.println("[Error] Already Stopped Music");
    }

    @Override
    public void stop(Player player)
    {
        // Kann nicht stoppen, da bereits gestoppt
        System.out.println("[Error] Already Stopped Music");
    }
}
```
<br>

Main:
```java
public class Main
{
    public static void main(String[] args)
    {
        Player player = new Player();

        // Kann nicht pausieren, da standardmäßig gestoppt
        player.pause();

        // Von stopped -> play
        player.play();

        // Von play -> paused
        player.pause();
    }
}
```

---

## Visitor

*(Hinweis: In der Originaldatei war dieser Abschnitt im Inhaltsverzeichnis aufgeführt, aber nicht ausformuliert – hier noch zu ergänzen.)*
