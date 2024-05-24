Week 2 - Functies en types
==========================
In de vorige les hebben we rekenkundige en logische expressies gezien. Daarnaast zijn lijsten en
operaties op lijsten aan bod gekomen. Tot slot hebben we gezien hoe we zelf functies kunnen maken en
aanroepen.

In het practicum bij de vorige les hebben we naast gehele getallen, logische expressies en lijsten
ook decimale getallen en tekst gezien. Er zijn dus verschillende types van expressies.
In deze les gaan we verder kijken naar deze types.


Na deze les kun je:
-------------------
* voor een gegeven expressie het type bepalen
* voor een gegeven functie het type bepalen
* de verschillen tussen een `List` en een `Tuple` uitleggen
* een functie ontwerpen (type bepalen en implementeren) voor een gegeven probleem


Types en waardes
----------------
Een type is de naam voor een verzameling van waardes met dezelfde eigenschappen.
* `Boolean` is de naam voor een type met 2 waardes: `true` en `false`.
* `Int` is de naam voor het type van alle gehele getallen: `-7`, `0`, `42`, etc.
* `String` is de naam voor het type van tekst: `""`, `"abc"`, `"Hello world!"`, `"123"`, etc.
* `Double` is de naam voor het type dat alle rationele getallen bevat: `-7.123`, `0.0`, `42.0`, `math.Pi`, `math.sqrt(2)`, etc.

In Scala schrijven we `x: Int` om vast te leggen dat `x` van het type `Int` is.
Soms moeten types in Scala expliciet worden opgeschreven, maar in veel gevallen kan de compiler
het type zelf afleiden.

In een Scala worksheet kan het type van een expressie als volgt worden gevonden
```text
1
val res0: Int = 1
```

In Scastie komt het type achter de expressie te staan
```text
1 // 1: scala.Int
```

In de vorige les en bij het practicum hebben we al een aantal types gezien:
* `Bool` - logische waardes
* `Char` - enkelvoudige karakters
* `String` - meerdere karakters samengevoegd
* `Int` - gehele getallen
* `Double` - komma-getallen

Als je probeert om 2 waardes van verschillende types probeert samen te voegen, krijg je een foutmelding,
een 'type error'. Het is dus belangrijk dat je altijd goed kijkt wat het type is!
```scala 3
1 + false // error; je kunt geen getal bij een boolean optellen
```


Lijsten
-------
Een `List` is een verzameling van waarden van **hetzelfde** type. Alle elementen in een lijst hebben
hetzelfde type. Bijv. in `List(1, 2, 3)` hebben alle elementen in de lijst het type `Int`. Het type
van de inhoud van de lijst noteren we tussen rechte haken: `List[Int]` of `List[Boolean]`.
Een lijst kan zelf ook lijsten bevatten, bijv. `List(List(1, 2, 3), List(4, 5, 6))` heeft het
type `List[List[Int]]`.

```text
List(false, true, false) // List[Boolean]

List(false, false) // List[Boolean]

List("abc", "def", "ghi", "jkl") // List[String]

List(List("abc"), List("def", "ghi")) // List[List[String]]
```

In de vorige les hebben we al verschillende manieren gezien om elementen uit een lijst te halen.

```scala 3
List(1, 2, 3).head // 1 : Int
List(1, 2, 3).tail // List(2, 3) : List[Int]
List(1, 2, 3)(1)   // 2 : Int    LET OP: met indexes tellen we vanaf 0, dus index 1 is eigenlijk het 2e element in de lijst!
List(1, 2, 3).last // 3 : Int
```

Merk op dat het type van een `List` niets zegt over de lengte van de lijst. Aan het type `List[String]`
kun je niet zien of de lijst leeg is, één element heeft, of meerdere elementen heeft. Ook zegt dit
type niets over de volgorde waarin de elementen staan. Zowel `List("a", "b", "c")` als
`List("c", "b", "a")` hebben het type `List[String]`.


Tuples
------
Een `Tuple` is een verzameling van waarden van **verschillende** types. We noteren een tuple als
kommagescheiden waarden, omringd door haken: `(false, 1, "hallo")`. Het type van een tuple wordt
bepaald door de waarden in het tuple. Voorgaand tuple heeft het type `(Boolean, Int, String)`.

Merk op dat het type van een tuple zowel de lengte als de volgorde van de waarden bepaald. Dat is
dus een verschil met een `List`!

```text
(false, true) // (Boolean, Boolean)

(true, false, true) // (Boolean, Boolean, Boolean)

(false, 'a', true) // (Boolean, Char, Boolean)

('a', (false, 'b')) // (Char, (Boolean, Char))

('a', List(false, true)) // (Char, List[Boolean])
```

Om elementen uit een tuple te krijgen, gebruik je in Scala de `_1`, `_2`, ... functies.
Let hierbij op: bij een lijst beginnen we met index 0 voor het eerste element, maar bij tuples
beginnen we bij 1 te tellen.

```scala 3
(1, true)._1 // 1 : Int
(1, true)._2 // true : Boolean
(1, "abc", 42)._3 // 42 : Int
```


EXTRA: `case class` - een tuple met een naam
-------------------------------------
Tuples worden in de praktijk vaak gebruikt om even wat tussentijdse resultaten op te slaan of door
te geven. Het is echter vaak lastig om later duidelijk te hebben wat de betekenis van een tuple is.
Daarom kiezen we er al snel voor om een tuple te vervangen door een class: een tuple met een naam
en waarin de waarden in het tuple zelf ook allemaal een naam hebben.

Aan een tuple als `(String, Int, Double)` kun je niet zien wat het is. Dat zou bijvoorbeeld
een persoon voor kunnen stellen met zijn/haar naam, leeftijd en het saldo op de bank, maar het kan net
zo goed een regel op een kassabon zijn met een omschrijving, aantal eenheden en de prijs per eenheid.

Je kunt hiervoor beter een `case class` gebruiken. Hierin geef je een naam aan de tuple én aan alle
onderdelen van de tuple, waardoor je duidelijk aangeeft wat de betekenis van het tuple is.

```scala 3
case class Product(omschrijving: String, aantal: Int, prijsPerEenheid: Double)
val product1 = Product("Karnemelk", 5, 0.95)
val product2 = Product("Ribbel Paprika Chips 335g", 1, 1.84)
```

Bij een tuple haal je met `_1` en `_2` de waarden uit je tuple. Bij een class gebruik je de namen
van de waarden om ze uit een object te halen.

```scala 3
val prijsProduct1 = product1.aantal * product1.prijsPerEenheid
val prijsProduct2 = product2.aantal * product2.prijsPerEenheid
```

Je kunt ook naar een `case class` refereren vanuit een andere `case class`. Hieronder zie je een voorbeeld
waarbij een `Adres` en een `Naam` is gedefinieerd, die vervolgens worden gebruikt in een `Persoon`.
Op deze manier kun je de data voor een model structureren en op een geordende manier opslaan.

```scala 3
case class Adres(straat: String, huisnummer: Int, postcode: String, plaats: String)
case class Naam(aanhef: String, voornaam: String, tussenvoegsel: String, achternaam: String)
case class Datum(dag: Int, maand: Int, jaar: Int)
case class Persoon(naam: Naam, adres: Adres, geboortedatum: Datum)

val jan = Persoon(
  Naam("dhr.", "Jan", "van", "Straaten"),
  Adres("Teststraat", "123", "1234AB", "Soest"),
  Datum(1, 2, 2003),
)

val jansVoornaam = jan.naam.voornaam
```


Functie types
-------------
Een functie neemt een waarde van een bepaald type en transformeert dat naar een waarde van hetzelfde
of een ander type. In de vorige les zagen we de functie `def dubbel(x: Int): Int` die het getal dat
je ingeeft, verdubbelt. In het practicum bij de vorige les zag je de functie
`def pythagoras(a: Double, b: Double): Double` die twee getallen inneemt en één getal teruggeeft.
En in het practicum bij deze les kom je de functie `def palindroom(s: String): Boolean` tegen,
die `true` teruggeeft wanneer `s` een palindroom is en `false` als dat niet zo is. Alle drie deze
voorbeelden nemen een waarde (of meerdere waarden) in als _input_ (ook wel _parameter_ of _argument_)
en transformeren die naar een _output_.

Het type van een functie noteren we als `t1 => t2`, waar `t1` de input en `t2` de _output_ van
de functie is. Je spreekt dit uit als "_een functie van t1 naar t2_".

```scala 3
def not(b: Boolean): Boolean = !b // not: Boolean => Boolean
def palindroom(s: String): Boolean = ??? // palindroom: String => Boolean
def generateNumber(): Int = 42 // generateNumber: () => Int
def add(x: Int, y: Int): Int = x + y // add: (Int, Int) => Int
```

De functie `not` heeft dus het type `Boolean => Boolean` en `palindroom` heeft type `String => Boolean`.
Functies kunnen 0 of meer input parameters hebben. De functie `generateNumber` heeft type
`() => Int` ("_Unit naar Int_") en de functie `add` heeft type `(Int, Int) => Int` (het input type
kun je hier eigenlijk zien als een tuple).


Afgeleide types
---------------
Bij een `val` hoef je in Scala nooit expliciet het type op te geven: de compiler kan dit zelf bepalen
naar aanleiding van de waarde die je eraan geeft.

```scala 3
val x: Int = 1
// het type is hierbij niet expliciet nodig
val x = 1
```

Dat is bij het output type van een functie ook het geval: je hoeft in de meeste gevallen het type
niet op te geven. In de functie `add` hierboven kan de compiler zelf uit de implementatie afleiden
dat het type `Int` teruggegeven wordt. Het type van de functie blijft nog steeds `(Int, Int) => Int`,
ook al schrijf je die laatste `Int` vaak niet expliciet in Scala.

```scala 3
def add(x: Int, y: Int) = x + y
```

Voor functie argumenten moet je wel altijd het type opgeven in Scala! `def add(x, y) = x + y` is
dus niet correct!


Generics
--------
Tot nu toe hebben we types van functies gezien die heel specifiek zijn. In het voorbeeld hieronder
kun je in `addInts` alleen maar waardes van het type `Int` geven en aan `stringLength` kun je niet
anders dan alleen iets van type `String` geven.

```scala 3
def addInts(x: Int, y: Int): Int = x + y
def stringLength(s: String): Int = s.length
```

Als we een functie willen maken die de lengte van een lijst berekent, dan kunnen we bijv.
`def length(xs: List[Int]): Int` gebruiken. Alleen kunnen we die functie dan uitsluitend gebruiken
voor `List[Int]` en niet voor `List[String]`! Voor het bepalen van de lengte van de lijst, maakt het
eigenlijk helemaal niet uit welk type waardes de lijst bevat. Of dat `Int`, `String`, of iets anders is,
doet niets met de lengte van de lijst. We kunnen het type van de lijst dan **generiek (Engels: generic)**
maken, waardoor we ieder soort lijst in de functie kunnen stoppen.

```scala 3
def length[A](xs: List[A]): Int
```

We maken de functie generiek door `[A]` toe te voegen. Het type van deze functie is nu `List[A] => Int`.
`A` kunnen we nu invullen met `Int`, `String`, of welk type we maar willen.

```scala 3
length(List(1, 3, 5, 7))
length(List("abc", "def"))
length(List(product1, product2)) // product1 en product2 zijn eerder gedefinieerd
```

Bij het aanroepen van `length` zoals hierboven hoeft het generieke type niet meegegeven te worden.
Net als met het output-type van een functie kan de compiler zelf bepalen wat het type voor `[A]` is.
Natuurlijk mag je dit type ook expliciet opgeven.

```scala 3
length[Int](List(1, 3, 5, 7))
length[String](List("abc", "def"))
length[Product](List(product1, product2))
```

Je kunt ook een waarde van een variabel type als output hebben:

```scala 3
def firstElement[A](xs: List[A]): A
```

Deze functie neemt een lijst van een willekeurig type als input en geeft het eerste element uit de
lijst terug en garandeert dat deze van datzelfde type is.

Voor `firstElement(List(1, 2, 3))` weten we dus dat hier een waarde van type `Int` uit komt en dat
deze zelfde functie een `String` teruggeeft bij `firstElement(List("abc", "def"))`.
