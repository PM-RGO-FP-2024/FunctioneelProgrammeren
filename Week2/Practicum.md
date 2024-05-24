Practicum - Week 2
==================
Dit practicum hoort bij de les over types en functies in Scala. Om onderstaande opdrachten uit te
voeren, kun je gebruik maken van [Scastie] of een Scala Worksheet als je bijv. [IntelliJ] hebt
geïnstalleerd op je eigen laptop.

**Deadline:** uiterlijk vrijdagmorgen 31 mei 2024 9:00 uur per mail inleveren bij de 3 docenten

Opdracht 0 - expressie types
----------------------------
Wat is het type van onderstaande expressies?
1. `List("a", "b", "c")`
2. `("a", "b", "c")`
3. `List((false , "0"), (true , "1"))`
4. `(List(false, true), List("0", "1"))`
5. `List((xs: List[Int]) => xs.tail, (xs: List[Int]) => xs.init, (xs: List[Int]) => xs.reverse)`
6. `((xs: List[Int]) => xs.tail, (xs: List[Int]) => xs.init, (xs: List[Int]) => xs.head, (xs: List[Int]) => xs.reverse)`
7. `(List(false, true), false)`
8. `("1,2","3,4")`
9. `List("false", "true")`
10. `List((1, true), (0, false))`

Opdracht 1 - functie types
--------------------------
Wat is het type van de onderstaande functies?
1. `def double(x: Int) = 2 * x`
2. `def second[A](xs: List[A]) = xs.tail.head`
3. `def swap[A, B](t: (A, B)) = (b, a)`
4. `def toList[A](t: (A, A, A)) = List(t._1, t._2, t._3)`

Opdracht 2 - functie aanroepen
------------------------------
Geef voor ieder van de functies uit Opdracht 1 een paar voorbeelden van hoe je deze kunt aanroepen
en wat de output is. Bijvoorbeeld: `second(List(3, 5, 7, 9))` geeft `5` en
`second(List(true, false, false true))` geeft `false`.

Opdracht 3 - tuple vs. list
---------------------------
In Opdracht 1.4 wordt met `toList` een `Tuple` omgezet naar een `List`.
1. Leg uit waarom het omgekeerde niet kan: een functie van een `List` naar een `Tuple`.
2. Leg uit waarom het tuple in het argument van de functie `toList` geen verschillende types kan hebben.

Opdracht 4 - functies definiëren
--------------------------------
Hieronder staan de implementaties van een aantal functies over lijsten. (1) Onderzoek voor iedere
implementatie wat ze doen. (2) Bedenk hier vervolgens een goed omschrijvende naam bij en maak een
functie rond de implementatie met het juiste type. (3) Geef ook een paar voorbeelden van hoe je die
functies zou aanroepen en wat dan de output daarbij is.
1. `xs.reverse.head`
2. `xs.tail.reverse`
3. `xs ++ ys`
4. `xs.drop(xs.length - 1).head`

Opdracht 5 - Palindroom
-----------------------
Een palindroom is een woord dat van voor naar achter hetzelfde is als van achter naar voren.
Voorbeelden: 'radar' en 'stormrots'. Schrijf een functie die controleert of een gegeven String
een palindroom is.

Hint: eerder heb je gezien hoe je een String van achter naar voren kunt krijgen en heb je ook gezien
hoe je twee Strings met elkaar vergelijkt.

```scala 3
def palindroom(s: String): Boolean = ???
```

Test je functie met een paar voorbeelden.
* `palindroom("anna")`
* `palindroom("piet")`
* `palindroom("12aba21")`
* `palindroom("stormrots")`

Opdracht 6 - Isogram
--------------------
Schrijf een functie die bepaalt of een woord een [isogram] is.
Hints:
* om de unieke letters in een woord te vinden, gebruik je `distinct`.
* om de lengte van een woord te vinden, gebruik je `length`
* om hoofdletters te vervangen door kleine letters, gebruik je `toLowerCase`

Test je functie met onderstaande voorbeelden:
* kleur
* kraan
* isogram
* vragenlijst
* Zwijndrecht
* filmproducent
* subdermatoglyphic

Opdracht 7 - Schrikkeljaar
--------------------------
In een schrikkeljaar zijn er 366 dagen in een jaar in plaats van 365 dagen. Of een jaar een schrikkeljaar
is, kun je bepalen aan de hand van het jaartal. Een jaar is een schrikkeljaar wanneer het jaartal
1. deelbaar is door 4
2. behalve als het deelbaar is door 100
3. maar wel als het deelbaar is door 400

Korte uitleg: https://youtu.be/xX96xng7sAE

Schrijf een functie die, gegeven een jaartal, teruggeeft of een jaar een schrikkeljaar is.

Test je functie met onderstaande voorbeelden:
* 1900 ==> nee
* 1964 ==> ja
* 2000 ==> ja
* 2020 ==> ja
* 2021 ==> nee
* 2022 ==> nee
* 2023 ==> nee
* 2024 ==> ja
* 1600 ==> ja
* 1700 ==> nee

EXTRA - Opdracht 8 - classes
----------------------------
Lees de sectie over [classes].

Stel: je werkt voor een bouwbedrijf en je moet een data-model voor de factuur opstellen.
Maak een aantal `case class`es die samen een factuur vormen. Maak daarnaast ook een paar voorbeeld
facturen met deze classes.

Een factuur heeft meestal een geadresseerde, een factuurdatum en -nummer, een lijst met producten
of geleverde diensten, een subtotaal, BTW, eventuele kortingen en een totaal. Houd er ook rekening
mee dat ieder product zijn eigen BTW percentage/bedrag kan hebben. Als je nog andere onderdelen van
een factuur bedenkt, voeg die dan ook toe aan je model en de voorbeelden.

[Scastie]: https://scastie.scala-lang.org/
[IntelliJ]: https://www.jetbrains.com/idea/
[isogram]: https://nl.wikipedia.org/wiki/Isogram
[classes]: README.md#extra-case-class---een-tuple-met-een-naam
