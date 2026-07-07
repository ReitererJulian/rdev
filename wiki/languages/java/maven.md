# Maven

## Inhaltsverzeichnis
* [Maven Erklärt](#maven-erklärt)
* [Warum Maven?](#warum-maven)
* [Maven Code](#maven-code)
* [Wichtigste POM Dependencys](#wichtigste-pom-dependencys)

---

Maven ist ein Projektmanagement- und Automatisierungstool für Java.
Man kann es sich wie einen digitalen Assistenten vorstellen, der verschiedene Aufgaben übernimmt.

<br>

## Maven Erklärt

`Dependency Management` (Abhängigkeitsverwaltung):

Eine Abhängigkeit wäre eine externe Bibliothek, z.B. für Tests oder Datenbanken.
Durch Maven muss man nicht extra die `.jar`-Datei manuell suchen und herunterladen.

<br>

`Standardisierte Struktur`:

Maven gibt eine feste Ordnerstruktur vor (z.B. `src/main/java/`).
Das macht es für andere einfacher, sich in deinem Projekt zurechtzufinden.

<br>

`Build Management` (automatisches Bauen):

Maven kompiliert Code, führt Tests aus und verpackt alles in eine fertige Datei (z.B. `.jar`).
Diese Datei kann man dann ausführen.

<br>

## Warum Maven?

Wie bereits gesagt, muss man durch `Maven` keine `.jar`-Dateien manuell in einen z.B. `lib`-Ordner legen.
Dadurch wird es auch einfacher, Code zu teilen.

## Maven Code

Also, wie fügt man `Dependencys` hinzu, und was sind die wichtigsten?

Jedes Maven-Projekt erstellt im Projekt-Home-Directory eine Datei.
Diese Datei heißt `pom.xml` (Project Object Model).

Diese Datei beschreibt:
* den Namen des Projekts
* die verwendete Java-Version
* die Dependencys

Beispiel:
```xml
<!-- XML-Deklaration und Festlegung der Zeichencodierung (UTF-8) -->
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!-- Organisation / Paketname -->
    <groupId>com.example</groupId>

    <!-- Name des Projektes -->
    <artifactId>ToDo</artifactId>

    <!-- Version der .jar-Datei -->
    <!-- SNAPSHOT -> noch in Entwicklung -->
    <version>1.0-SNAPSHOT</version>

    <properties>
        <!-- Variablen, die man wiederverwenden kann -->
        <maven.compiler.source>24</maven.compiler.source>
        <maven.compiler.target>24</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <junit.version>5.10.0</junit.version>
    </properties>

    <!-- Hier stehen alle externen Libraries -->
    <dependencies>

        <!-- JUnit (zum Testen) -->
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>${junit.version}</version>
            <scope>test</scope>
        </dependency>

        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-engine</artifactId>
            <version>${junit.version}</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

</project>
```

### Wichtigste POM Dependencys

JUnit:
```xml
<properties>
    <junit.version>5.10.0</junit.version>
</properties>

<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>${junit.version}</version>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-engine</artifactId>
        <version>${junit.version}</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```
<br>

Logger (SLF4J + Logback):
```xml
<properties>
    <slf4j.version>2.0.13</slf4j.version>
    <logback.version>1.5.6</logback.version>
</properties>

<dependencies>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>${slf4j.version}</version>
    </dependency>

    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>${logback.version}</version>
    </dependency>
</dependencies>
```

---

## Offene Punkte (noch nicht ausformuliert)

* Build to .jar
* Make a .exe
* Make a CLI
* Make a UI
* Connect a DB
