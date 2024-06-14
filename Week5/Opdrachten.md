Practicum - Week 5
==================
Dit practicum hoort bij de les over "_Recursie_".
Om onderstaande opdrachten uit te voeren, kun je gebruik maken van [Scastie] of een Scala Worksheet
als je bijv. [IntelliJ] hebt geïnstalleerd op je eigen laptop.

**Deadline:** uiterlijk vrijdagmorgen 21 juni 2024 9:00 uur per mail inleveren bij de 3 docenten

Opdracht 0 - Driehoeksgetal
---------------------------
Maak een recursieve functie die de som van de getallen `0` t/m `n` berekent met `n >= 0`. Dit wordt
ook wel een [driehoeksgetal] genoemd. Natuurlijk kun je dit doen met `(0 to n).sum`, maar in deze
opdracht moet je het recursief doen. Voorbeeld: `driehoek(4) = 4 + 3 + 2 + 1 + 0 = 10`.

```scala 3
def driehoek(n: Int): Int = n match {
  case 0 => ???
  case n => ???
}
```

Test je functie met `driehoek(4)` in Scastie. En wat is `driehoek(500)`?

Opdracht 1 - `replicate`
------------------------
In het practicum van week 4 heb je de functie `replicate` geïmplementeerd middels een
for-comprehension. Doe dit opnieuw, maar nu met recursie over `i`.  De functie
`def replicate[A](i: Int, a: A): List[A]` genereert een lijst van lengte `i` met identieke elementen
`a` zodat bijv. `replicate(3, true)` het resultaat `[true, true, true]` geeft.

Opdracht 2 - Algoritme van Euclides
-----------------------------------
Het Algoritme van Euclides is een manier om de grootste gemene deler van twee positieve gehele
getallen te vinden. Het algoritme vermindert het grootste van de twee getallen herhaaldelijk met
het kleinste van de twee getallen totdat de getallen gelijk zijn. Dat is het resultaat dat wordt
teruggegeven.

Voorbeelden:
```text
euclid(5, 7) = euclid(5, 2) = euclid(3, 2) = euclid(1, 2) = euclid(1, 1) = 1
euclid(4, 2) = euclid(2, 2) = 2
```

Implementeer de functie `def euclid(a: Int, b: Int): Int` middels recursie. Test je implementatie
met verschillende inputs.

Bereken `euclid(13404, 8832)`

Opdracht 3 - `contains`
-----------------------
De functie `def contains[A](list: List[A], elem: A): Boolean` geeft `true` wanneer `elem` in `list`
zit en `false` als dat niet het geval is. Implementeer deze functie middels recursie. Test je
implementatie met verschillende inputs.

Opdracht 4 - `drop`
-------------------
In de les hebben we de functie `take` geïmplementeerd middels recursie. Neem de code daarvan over en
pas die aan om de functie `def drop[A](list: List[A], n: Int): List[A]` te implementeren. Test je
implementatie met verschillende inputs. Jouw implementatie zou hetzelfde moeten werken als de
`list.drop(n)` die je in Week 1 hebt gezien.

Opdracht 5 - `zip`
------------------
De functie `def zip[A, B](as: List[A], bs: List[B]): List[(A, B)]` combineert de lijsten `as` en `bs`
in een lijst van tuples. Bijv. `zip(List(1, 2, 3), List("abc", "def", "ghi"))` resulteert in
`List((1, "abc"), (2, "def"), (3, "ghi"))`. Als de twee lijsten niet even lang zijn, bevat het
resultaat van `zip(as, bs)` net zoveel elementen als de kortste lijst:
`zip(List(1, 2, 3), List("abc"))` is `List((1, "abc"))`.

Implementeer `zip` middels recursie over de twee lijsten. Bedenk dat er in dit geval 2 basis-gevallen
zijn!

Evaluatie
---------
Schrijf **individueel** een korte evaluatie van deze module Functioneel Programmeren.
Wat heb je geleerd in deze module? Hoe vond je dat de lessen verliepen? Wat vond je van de practica?
Welke onderdelen vond je makkelijk of juist moeilijk? Hoe zouden we deze module in een volgende jaargang
kunnen verbeteren?

Eindopdracht - Creditcard validatie
-----------------------------------
Wanneer je bij een webshop iets besteld, kun je betalen met een creditcard. Om te controleren of
een creditcard-nummer geldig is, wordt vaak gebruik gemaakt van een algoritme. In deze opdracht
ga je een deel van dit algoritme implementeren.

Het algoritme bestaat uit de volgende stappen:
* verdubbel de waarde van ieder tweede cijfer van het creditcard-nummer, doe dit van rechts naar links
* tel de cijfers van de verdubbelde getallen en onverdubbelde cijfers van het originele creditcard-nummer bij elkaar op
* als deze som deelbaar is door 10, is het creditcard-nummer geldig.

Hier is een voorbeeld voor het creditcard-nummer `4012888888881881`.
* om van rechts naar links te verdubbelen
  * zetten we het getal eerst om in een lijst: `List(4, 0, 1, 2, 8, 8, 8, 8, 8, 8, 8, 8, 1, 8, 8, 1)`
  * ...en draaien die vervolgens om: `List(1, 8, 8, 1, 8, 8, 8, 8, 8, 8, 8, 8, 2, 1, 0, 4)`
* vervolgens verdubbelen we ieder tweede getal: `List(1, 16, 8, 2, 8, 16, 8, 16, 8, 16, 8, 16, 2, 2, 0, 8)`
* om de som van alle cijfers te berekenen, moeten we eerst de getallen groter dan 9 opsplitsen in losse cijfers: `List(1, 1, 6, 8, 2, 8, 1, 6, 8, 1, 6, 8, 1, 6, 8, 1, 6, 2, 2, 0, 8)`
* als we al deze getallen optellen, komen we uit op `90`
* `90 % 10 == 0`, dus 90 is deelbaar door 10 en dus is dit een geldig creditcard-nummer!

In onderstaande taken implementeer je een aantal functies die corresponderen met de verschillende stappen
zoals hierboven in het voorbeeld omschreven. Aan het einde kun je al deze functies gebruiken om te bepalen
of een creditcard-nummer geldig is.

### `toDigits`
Implementeer de functie `def toDigits(creditcardNummer: String): List[Int]` die een creditcard-nummer
omzet naar een lijst van getallen, zodat `toDigits("4012888888881881") = List(4, 0, 1, 2, 8, 8, 8, 8, 8, 8, 8, 8, 1, 8, 8, 1)`

**Hint:**
* gebruik een for-comprehension om over de karakters in de lijst te itereren
* gebruik `c.asDigit` om een karakter `c` om te zetten naar het cijfer van type `Int`

**Vraag:**
Evalueer `toDigits("123456")`

### `toDigitsReverse`
Implementeer de functie `def toDigitsReverse(creditcardNummer: String): List[Int]` die een creditcard-nummer
omzet naar de omgekeerde lijst van getallen, zodat `toDigitsReverse("4012888888881881") = List(1, 8, 8, 1, 8, 8, 8, 8, 8, 8, 8, 8, 2, 1, 0, 4)`

**Hint:**
* Gebruik de `toDigits` van hierboven

**Vraag:**
Evalueer `toDigitsReverse("123456")`

### `doubleSecond`
Implementeer de functie `def doubleSecond(list: List[Int]): List[Int]` die ieder tweede getal in de lijst
verdubbelt. Bijv. `doubleSecond(List(8, 7, 6, 5)) = List(8, 14, 6, 10)`

**Hint:**
* Gebruik pattern matching en recursie over `list`
* Er zijn 2 basis-gevallen en één algemeen geval

**Vraag:**
Evalueer de volgende expressies:
* `doubleSecond(List())`
* `doubleSecond(List(5))`
* `doubleSecond(List(2, 5))`
* `doubleSecond(List(2, 5, 3, 6))`

### `sumDigits`
Implementeer de functie `def sumDigits(list: List[Int]): Int` die de cijfers van de waarden in `list` bij
elkaar optelt. Bijv. `sumDigits(List(8, 14, 6, 10)) = 8 + (1 + 4) + 6 + (1 + 0) = 20`

**Hint:**
* Gebruik een for-comprehension
* Gebruik de functie `toDigits` van hierboven om de cijfers in een getal groter dan 9 los van elkaar te krijgen

**Vraag:**
Evalueer de volgende expressies:
* `sumDigits(List())`
* `sumDigits(List(5))`
* `sumDigits(List(6, 66, 666))`

### `deelbaarDoorTien`
Implementeer de functie `def deelbaarDoorTien(getal: Int): Boolean` die `true` teruggeeft als `getal`
deelbaar is door 10 en `false` als dat niet het geval is. Test je implementatie met een paar voorbeelden.

### `isValid`
Om een creditcard-nummer te valideren, moet je bovenstaande functies combineren. Implementeer de functie

```scala 3
def isValid(creditcardNummer: String): Boolean = ???
```

Evalueer de volgende expressies:
* `isValid("5256283618614517")`
* `isValid("4556945538735694")`
* `isValid("0000000000000000")`

### Hoeveel creditcards zijn geldig?
Je kunt dit algoritme gebruiken om voor een lijst met creditcard-nummers te valideren hoeveel er
geldig zijn. Hieronder staat zo'n lijst én de functie `numValid` die telt hoeveel van deze creditcards
geldig zijn. Gebruik de code hierboven om te bepalen wat de waarde is voor `numValid(creditcards)`?

```scala 3
def numValid(creditcardNummers: List[String]): Long = (for {
  nummer <- creditcardNummers
  if isValid(nummer)
} yield 1).sum

val creditcards = List(
  "4716347184862961", "4532899082537349", "377851536227201", "345763240913232",
  "4485429517622493", "4320635998241421", "4929778869082405", "5256283618614517",
  "5507514403575522", "5191806267524120", "5396452857080331", "5567798501168013",
  "6011798764103720", "6011970953092861", "6011486447384806", "6011337752144550",
  "6011442159205994", "4916188093226163", "4916699537435624", "4024607115319476",
  "4556945538735693", "4532818294886666", "5349308918130507", "5156469512589415",
  "5210896944802939", "5442782486960998", "5385907818416901", "6011920409800508",
  "6011978316213975", "6011221666280064", "6011285399268094", "6011111757787451",
  "4024007106747875", "4916148692391990", "4916918116659358", "4024007109091313",
  "4716815014741522", "5370975221279675", "5586822747605880", "5446122675080587",
  "5361718970369004", "5543878863367027", "6011996932510178", "6011475323876084",
  "6011358905586117", "6011672107152563", "6011660634944997", "4532917110736356",
  "4485548499291791", "4532098581822262", "4018626753711468", "4454290525773941",
  "5593710059099297", "5275213041261476", "5244162726358685", "5583726743957726",
  "5108718020905086", "6011887079002610", "6011119104045333", "6011296087222376",
  "6011183539053619", "6011067418196187", "4532462702719400", "4420029044272063",
  "4716494048062261", "4916853817750471", "4327554795485824", "5138477489321723",
  "5452898762612993", "5246310677063212", "5211257116158320", "5230793016257272",
  "6011265295282522", "6011034443437754", "6011582769987164", "6011821695998586",
  "6011420220198992", "4716625186530516", "4485290399115271", "4556449305907296",
  "4532036228186543", "4916950537496300", "5188481717181072", "5535021441100707",
  "5331217916806887", "5212754109160056", "5580039541241472", "6011450326200252",
  "6011141461689343", "6011886911067144", "6011835735645726", "6011063209139742",
  "379517444387209", "377250784667541", "347171902952673", "379852678889749",
  "345449316207827", "349968440887576", "347727987370269", "370147776002793",
  "374465794689268", "340860752032008", "349569393937707", "379610201376008",
  "346590844560212", "376638943222680", "378753384029375", "348159548355291",
  "345714137642682", "347556554119626", "370919740116903", "375059255910682",
  "373129538038460", "346734548488728", "370697814213115", "377968192654740",
  "379127496780069", "375213257576161", "379055805946370", "345835454524671")
```

[Scastie]: https://scastie.scala-lang.org/
[IntelliJ]: https://www.jetbrains.com/idea/
[driehoeksgetal]: https://nl.wikipedia.org/wiki/Driehoeksgetal
