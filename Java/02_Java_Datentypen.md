# 02 Java Datentypen

## Einleitung
Datentypen sind Schemen für die Verwendung von [Bits](../resources/glossary.md#bit). Mit ihnen lassen sich Werte, abhängig von der Größe der jeweiligen Datentypen, darstellen. Z.B. ist eine Ganzzahl ein anderer Datentyp als eine Fließkommazahl.

## Datentypen
Grundsätzlich wird zwischen 2 Arten von Datentypen unterschieden.

- [Primitive Datentypen](#primitive-datentypen)
- [Referenzdatentypen](#referenzdatentypen)

### Primitive Datentypen
Primitive Datentypen werden auch einfache oder elementare Datentypen genannt. In Java existieren nur 8 solcher Datentypen. Die folgende Tabelle zeigt eine Übersicht aller primitiven Datentypen.

| Datentyp  | Kategorie           | [Wrapper-Klasse](../resources/glossary.md#wrapper-class) | Größe in Bit                                                                                                                                                                                                                                                                                                    | Wertebereich                                                                                             | Beschreibung                                                                                  |
|-----------|---------------------|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| `byte`    | Ganzzahlig          | `java.lang.Byte`                                         | 8                                                                                                                                                                                                                                                                                                               | -128 bis +127                                                                                            | Zweierkomplement-Werte                                                                        |
| `short`   | Ganzzahlig          | `java.lang.Short`                                        | 16                                                                                                                                                                                                                                                                                                              | -32.768 bis +32.767                                                                                      | Zweierkomplement-Werte                                                                        |
| `int`     | Ganzzahlig          | `java.lang.Integer`                                      | 32                                                                                                                                                                                                                                                                                                              | -2.147.483.648 bis +2.147.483.647                                                                        | Zweierkomplement-Werte                                                                        |
| `long`    | Ganzzahlig          | `java.lang.Long`                                         | 64                                                                                                                                                                                                                                                                                                              | -9.223.372.036.854.775.808 bis +9.223.372.036.854.775.807                                                | Zweierkomplement-Werte                                                                        |
| `float`   | Gleitkommazahl      | `java.lang.Float`                                        | 32                                                                                                                                                                                                                                                                                                              | -3,40282347 * 10<sup>38</sup> bis +3,40282347 * 10<sup>38</sup> (8 Nachkommastellen)                     | 32-Bit [IEEE 754](../resources/glossary.md#ieee-754)-Gleitkommazahl                           |
| `double`  | Gleitkommazahl      | `java.lang.Double`                                       | 64                                                                                                                                                                                                                                                                                                              | -1,79769313486231570 * 10<up>308</sup> bis +1,79769313486231570 * 10<sup>308</sup> (17 Nachkommastellen) | 64-Bit [IEEE 754](../resources/glossary.md#ieee-754)-Gleitkommazahl mit doppelter Genauigkeit |
| `char`    | Character-Datentyp  | `java.lang.Character`                                    | 16                                                                                                                                                                                                                                                                                                              | 0 bis +65.535                                                                                            | Unicode-Zeichen (UTF-16)                                                                      |
| `boolean` | Boolescher Datentyp | `java.lang.Boolean`                                      | Abhängig von der <tooltip term="JVM"><format color="orange">JVM</format></tooltip>. Theoretisch 1 Bit, praktisch 1 Byte (8 Bit), da dies der minimal adressierbare Speicherblock ist. (Der Overhead für das Ansprechen von weniger als einem Byte überwiegt häufig den Vorteil des geringeren Speicherbedarfs.) | `true` oder `false`                                                                                      | Boolescher Wahrheitswert                                                                      |

#### Ganzzahlen

> [!CAUTION]
> Vorsicht bei der Verwendung von Ganzzahlen, welche außerhalb des Wertebereichs von `int` liegen.
> ```java
> System.out.println(8273469237); // Compiler-Fehler!
> ```

Der [Compiler](../resources/glossary.md#compiler) interpretiert solche [Literale](01_Java_Token.md#literale) standardmäßig als Integer-Ganzzahlen. Damit der Compiler erkennt, dass es sich um einen Datenwert vom Typ `long` handelt, muss dies mit einem `L` am Ende gekennzeichnet werden.

> [!CAUTION]
> ```java
> System.out.println(8273469237);

> [!TIP]
> ```java
> System.out.println(8273469237L);

> [!NOTE]
> `System.out.println()` wird für die Ausgabe auf der Konsole verwendet – siehe <a href="04_Java_Ein_Ausgaben.md">Kapitel 4 – Ein- und Ausgaben</a>.

Neben der standardmäßig ganzzahligen Schreibweise, kann auch die binäre, oktale oder hexadezimale Schreibweise verwendet werden.

| Zahlensystem | Präfix |
|--------------|--------|
| Binär        | `0b`   |
| Oktal        | `0`    |
| Hexadezimal  | `0x`   |

Folgendes Beispiel zur Veranschaulichung. Die Syntax wird im nachfolgenden [Kapitel 3 – Variablen](03_Java_Variablen.md) genauer erklärt.

```java
int decimal = 42;  
int binary = 0b1101;  
int octal = 023;  
int hexadecimal = 0x2B;
```

#### Gleitkommazahlen

Um Gleitkommazahlen darstellen zu können, wurden die Datentypen `float` und `double` eingeführt. Soll der Restwert berechnet werden, wird dafür der Operator `%` verwendet. Das folgende Beispiel zeigt 4 Varianten für die Kennzeichnung einer Kommazahl.

```java
System.out.println(1 / 10.0);
System.out.println(1 / 10.);
System.out.println(1 / 10f);
System.out.println(1 / 10d);
```

> [!CAUTION]
> Was wird bei folgendem Beispiel auf der Konsole ausgegeben?
> ```java
> System.out.println(1 / 10);

> [!TIP]
> Regulär würde man im Kopf auf das Ergebnis `0.1` kommen. Da in Java jedoch standardmäßig mit Ganzzahlen gearbeitet wird, wird alles, was nach dem Komma steht abgeschnitten. Das Ergebnis ist also `0`.
> 
> Wenn das Ergebnis als Kommazahl vorliegen soll, muss bei mindestens einer der beiden Operanden angegeben werden, dass es sich bei dessen Datentyp um eine Kommazahl handelt.

> [!CAUTION]
> Was ergibt `0.1 + 0.2`?

```java
~0.30000000000000004
```

> [!CAUTION]
> Da der Computer nur `0` und `1` versteht, kann es beim Rechnen mit Gleitkommazahlen zu minimalen Abweichungen kommen. Dies ist jedoch kein Problem von Java, sondern von Programmiersprachen/CPUs allgemein und liegt an einer ungünstigen Binärdarstellung.

> [!NOTE]
> Ein zu empfehlendes Video über die Gleitkommazahlenproblematik, ist <a href="https://www.youtube.com/watch?v=PZRI1IfStY0">hier</a> zu finden.

Gleitkommazahlen können auch die wissenschaftliche Notation repräsentieren. Diese kann direkt angewendet werden.

```java
double d = 1e-10;
```

#### Datentyp `char`

Der Datentyp `char` ist für die Darstellung eines einzelnen Zeichens verantwortlich. `char` steht als Abkürzung für `character`. Intern werden die Zeichen als Unicode (16-Bit-Dualzahl) dargestellt. Mit anderen Worten: Jedes Zeichen repräsentiert intern eine Ganzzahl. Daher kann ein `char` auch als `int` gespeichert werden.

```java
int at1 = '@';
char at2 = '@';
System.out.println(at1);  // 64
System.out.println(at2);  // @
```

##### Escape Sequenzen

Der [Compiler](../resources/glossary.md#compiler) interpretiert einige Zeichen als Escape Sequenzen. Folgende Tabelle zeigt alle möglichen Escape Sequenzen.

| Escape Sequenz | Beschreibung                    |
|----------------|---------------------------------|
| `\t`           | Horizontaler Tabulator          |
| `\r`           | Carriage Return (Wagenrücklauf) |
| `\n`           | Zeilenumbruch                   |
| `\uXXXX`       | Unicode XXXX (hexadezimal)      |
| `\b`           | Backspace (Rückschritt)         |
| `\f`           | Form Feed (Seitenumbruch)       |
| `\'`           | Hochkommata                     |
| `\"`           | Anführungszeichen               |
| `\\`           | Backslash                       |

#### Datentyp `boolean`

Vergleiche werden mit dem Typ `boolean` realisiert. Beispielsweise um zu prüfen, ob eine Zahl größer ist, als eine andere. Die einzigen [Literale](01_Java_Token.md#literale) die ein `boolean` annehmen kann, sind `true` (wahr) oder `false` (falsch).

```java
boolean isRunning = false;
boolean isJumping = true;
```

### Referenzdatentypen

Referenzdatentypen werden im Verlauf der späteren Kapitel genauer beschrieben. Ein Referenzdatentyp, auch Objekt genannt, kann im Grunde alles sein, was einem in den Sinn kommt. Beispielsweise ein Ball, ein Mensch, eine Aktivität oder sogar eine Dimension. Solche Objekte werden durch Eigenschaften (Objektvariablen) und Funktionalitäten (Objektmethoden) beschrieben.

- Methoden stellen dabei die Funktionen eines Objekts dar. Ein Mensch kann z.B. gehen ([Kapitel 9 – Methoden](09_Java_Methoden.md)).
- Objektvariablen speichern zu jedem Objekt spezifische Eigenschaften. Ein Mensch hat z.B. ein Alter und einen Namen ([Kapitel 10 – Klassen: Objektvariablen](10_Java_Klassen.md)).
- Auf Objekte wird in [Kapitel 11 – Objekte](11_Java_Objekte.md) & [Kapitel 14 – OOP](14_Java_OOP.md) genauer eingegangen.
- Auf zwei bestimmte Objekte wird bereits früher in [Kapitel 5 – Zeichenketten](05_Java_Zeichenketten.md) und [Kapitel 8 – Arrays](08_Java_Arrays.md) eingegangen.