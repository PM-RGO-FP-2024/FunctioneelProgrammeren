Practicum - Week 4
==================
Dit practicum hoort bij de les "_Itereren over collecties_".
Om onderstaande opdrachten uit te voeren, kun je gebruik maken van [Scastie] of een Scala Worksheet
als je bijv. [IntelliJ] hebt geïnstalleerd op je eigen laptop.

**Deadline:** uiterlijk vrijdagmorgen 14 juni 2024 9:00 uur per mail inleveren bij de 3 docenten

Opdracht 0 - Kwadraten
----------------------
Schrijf een for-comprehension die een lijst van de eerste 10 kwadraten produceert:
`[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]`

Opdracht 1 - Replicate
----------------------
De functie `def replicate[A](i: Int, a: A): Seq[A]` genereert een lijst van lengte `i` met
identieke elementen `a` zodat bijv. `replicate(3, true)` het resultaat `[true, true, true]` geeft.
Implementeer deze functie met een for-comprehension.

Opdracht 2 - Pythagoras
-----------------------
Een 3-tuple `(x, y, z)` van positieve integers is Pythagorisch wanneer `x^2 + y^2 = z^2`.
Hieronder staan 4 implementaties van de functie `pyths`. Welke implementatie geeft een lijst van
alle Pythagorische 3-tuples waarvan de onderdelen kleiner zijn dan de opgegeven limiet?
Bijv. `pyths(10)` geeft `[(3, 4, 5), (4, 3, 5), (6, 8, 10), (8, 6, 10)]`
Leg voor de correcte implementatie uit wat deze doet en leg vervolgens voor de andere implementaties
uit waarom deze niet correct zijn.

```scala 3
def pyths1(n: Int): Seq[(Int, Int, Int)] = for {
  x <- 1 to n
  y <- 1 to x
  z <- 1 to y
  if x*x + y*y == z*z
} yield (x, y, z)
```

```scala 3
def pyths2(n: Int): Seq[(Int, Int, Int)] = for {
  x <- 1 to n
  y <- x to n
  z <- y to n
  if x*x + y*y == z*z
} yield (x, y, z)
```

```scala 3
def pyths3(n: Int): Seq[(Int, Int, Int)] = for {
  x <- 1 to n
  y <- 1 to n
  z <- 1 to n
  if x*x + y*y == z*z
} yield (x, y, z)
```

```scala 3
def pyths4(n: Int): Seq[(Int, Int, Int)] = for {
  x <- 1 to n
  y <- 1 to n
} yield (x, y, x*x + y*y)
```

Opdracht 3 - Perfecte getallen
------------------------------
Een positief geheel getal noemen we "perfect" wanneer het gelijk is aan de som van zijn factoren,
behalve het getal zelf. Implementeer de functie `perfect(n: Int): Boolean` die teruggeeft of een
getal "perfect" is.

Hint: gebruik de functie `factoren` die we tijdens de les hebben gemaakt.
Test je implementatie met een paar voorbeelden. 6 en 28 zijn voorbeelden van perfecte getallen.

Implementeer vervolgens de functie `perfects(max: Int)` die de perfecte getallen teruggeeft
die kleiner zijn dan of gelijk zijn aan `max`.

Voorbeeld: `perfects(500)` geeft `[6, 28, 496]`

Opdracht 4 - Zoek de waarde
---------------------------
Implementeer een functie `find` die gegeven een lijst van tuples en een key, een lijst met values
teruggeeft die hetzelfde zijn als die key.

```scala 3
def find[A, B](key: A, list: List[(A, B)]): List[B] = ???
```

Voorbeeld: `find("a", List(("b", 1), ("a", 2), ("c", 3), ("a", 4)))` geeft terug `List(2, 4)`
en `find("a", List(("b", 1)))` geeft terug `List()`

Onderzoek vervolgens wat de functie `zipWithIndex` doet voor een lijst. Gebruik hiervoor ook de
[documentatie](https://www.scala-lang.org/api/current/scala/collection/immutable/List.html#zipWithIndex-0).
Experimenteer met hoe je deze functie kunt gebruiken.

Implementeer tot slot de functie `positions` die gegeven een lijst en een key,
de lijst met indexes teruggeeft waarop de key in de lijst voorkomt. Gebruik hiervoor de functie
`find` die je eerst hebt geïmplementeerd en `zipWithIndex`.

```scala 3
def positions[A](key: A, list: List[A]): List[Int] = ???
```

Voorbeeld: `positions(3, List(1, 3, 5, 3, 9, 5, 3))` geeft `List(1, 3, 6)`

Opdracht 5 - Tafels van vermenigvuldiging
-----------------------------------------
In deze opdracht ga je een programma schrijven dat een tabel produceert waarmee je de tafels van
1 t/m 10 kunt aflezen.

```text
   1   2   3   4   5   6   7   8   9  10
   2   4   6   8  10  12  14  16  18  20
   3   6   9  12  15  18  21  24  27  30
   4   8  12  16  20  24  28  32  36  40
   5  10  15  20  25  30  35  40  45  50
   6  12  18  24  30  36  42  48  54  60
   7  14  21  28  35  42  49  56  63  70
   8  16  24  32  40  48  56  64  72  80
   9  18  27  36  45  54  63  72  81  90
  10  20  30  40  50  60  70  80  90 100
```

Gebruik hierbij de volgende template:
```scala 3
def createRowNumbers(row: Int): Seq[Int] = ???

def formatNumber(number: Int): String = " " * (4 - number.toString.length) + number

def createRow(row: Int): Seq[String] = ???
def createRowString(row: Int): String = ???

def createRows(): Seq[String] = ???
def createTable(): String = ???
```

Implementeer de functie `createRowNumbers`, die de getallen uit de gegeven rij teruggeeft.
Bijv. `createRowNumbers(4)` geeft de lijst `[4, 8, 12, 16, 20, 24, 28, 32, 36, 40]`

Vervolgens moeten we de getallen in de rij formatteren zodat ze allemaal netjes onder elkaar komen
te staan in de kolommen en de tabel goed uit te lezen is. Hiervoor gebruiken we de functie `formatNumber`.
Probeer deze functie uit met verschillende getallen. Leg vervolgens in je eigen woorden uit hoe deze
functie precies werkt.

Combineer de functies `createRowNumbers` en `formatNumber` in de functie `createRow`, die gegeven
een rijnummer de lijst van geformatteerde getallen als `String`s teruggeeft.

In `createRowString` worden de getallen uit een rij vervolgens aan elkaar geplakt tot één `String`.
Gebruik hiervoor `createRow` en herinner je de `mkString` functie(s) uit het huiswerk van week 0.
Test dat `createRowString(4)` het volgende resultaat geeft: `"   4   8  12  16  20  24  28  32  36  40"`

Implementeer `createRows`, die de functie `createRowString` gebruikt om voor alle 10 de rijen de juiste
`String` in een lijst terug te geven.

Combineer deze `Seq[String]` vervolgens tot één `String` door de rijen aan elkaar te plakken op nieuwe
regels. Gebruik hiervoor opnieuw `mkString`.
Hint: gebruik `"\n"` als scheidingsteken tussen de `String`s om ze op nieuwe regels te krijgen.

Opdracht 6 - Sudoku prettyprinter
---------------------------------
Een sudoku puzzel bestaat uit een 9x9 grid waarin de getallen 1 t/m 9 moeten worden ingevuld zodat:
* iedere rij precies 1x deze getallen bevat
* iedere kolom precies 1x deze getallen bevat
* iedere 3x3 box precies 1x deze getallen bevat

We kunnen een sudoku puzzel beschrijven als een array van arrays van integers. Hierbij noteren we
de lege cellen met een `0`. Hieronder zie je hiervan een voorbeeld:

```scala 3
type Sudoku = Array[Array[Int]]

val problem: Sudoku =
  Array(
    Array(5, 3, 0, 0, 7, 0, 0, 0, 0),
    Array(6, 0, 0, 1, 9, 5, 0, 0, 0),
    Array(0, 9, 8, 0, 0, 0, 0, 6, 0),
    Array(8, 0, 0, 0, 6, 0, 0, 0, 3),
    Array(4, 0, 0, 8, 0, 3, 0, 0, 1),
    Array(7, 0, 0, 0, 2, 0, 0, 0, 6),
    Array(0, 6, 0, 0, 0, 0, 2, 8, 0),
    Array(0, 0, 0, 4, 1, 9, 0, 0, 5),
    Array(0, 0, 0, 0, 8, 0, 0, 7, 9),
  )
```

Schrijf in deze opdracht een serie functies die een sudoku als een `String` formatteert, inclusief de
horizontale en verticale lijnen.

```scala 3
def prettyprint(sudoku: Sudoku): String = ???
```

Gebruik hiervoor:
* for-comprehensions
* `mkString`
* `List(1, 2, 3, 4, 5, 6, 7, 8, 9).grouped(3)` geeft een `List(List(1, 2, 3), List(4, 5, 6), List(7, 8, 9))`

Het aanroepen van `prettyprint(problem)` geeft het volgende resultaat:

```text
+-------+-------+-------+
| 5 3 _ | _ 7 _ | _ _ _ |
| 6 _ _ | 1 9 5 | _ _ _ |
| _ 9 8 | _ _ _ | _ 6 _ |
+-------+-------+-------+
| 8 _ _ | _ 6 _ | _ _ 3 |
| 4 _ _ | 8 _ 3 | _ _ 1 |
| 7 _ _ | _ 2 _ | _ _ 6 |
+-------+-------+-------+
| _ 6 _ | _ _ _ | 2 8 _ |
| _ _ _ | 4 1 9 | _ _ 5 |
| _ _ _ | _ 8 _ | _ 7 9 |
+-------+-------+-------+
```

[Scastie]: https://scastie.scala-lang.org/
[IntelliJ]: https://www.jetbrains.com/idea/
