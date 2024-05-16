Practicum - Week 1
===================
Dit practicum hoort bij de eerste les over functioneel programmeren. In de les hebben we een
aantal eenvoudige expressies en functies in Scala gezien. Om onderstaande opdrachten uit te voeren,
kun je gebruik maken van [Scastie] of een Scala Worksheet als je bijv. [IntelliJ] hebt geïnstalleerd
op je eigen laptop.

**Deadline:** uiterlijk vrijdagmorgen 24 mei 2024 9:00 uur per mail inleveren bij de 3 docenten

Opdracht 0 - Integers
---------------------
Evalueer de volgende expressies.
Leg uit wat het verschil tussen deze expressies is. Let op: niet alle expressies zijn correct!
1. `6 * 11 - 2`
2. `(6 * 11) - 2`
3. `6 * (11 - 2)`
4. `6 * (11 - 2`

Opdracht 1 - Booleans
---------------------
Evalueer de volgende expressies.
1. `true || false`
2. `false && true`
3. `true && true`
4. `!false && true`
5. `!(false && true)`
6. `!(false || true)`
7. `(!false || true) && (false || true)`

Opdracht 2 - List operaties
---------------------------
Evalueer de volgende expressies over lijsten. Leg uit wat de expressie doet. Evalueer de expressie
vervolgens "uit je hoofd" en controleer daarna pas in Scastie of IntelliJ.
1. `List(4, 6, 9, 1).take(2)`
2. `List(4, 6, 9, 1, 8, 5, 3).drop(3)`
3. `List(4, 6, 9, 1).head`
4. `List(4, 6, 9, 1).tail`
5. `List(4, 6, 9, 1, 8, 5, 3).reverse`
6. `List(4, 6, 9, 1, 8, 5, 3).sorted`
7. `List(4, 6, 9, 1, 8, 4, 1, 5, 6).distinct`
8. `List(4, 6, 9, 1, 8, 5, 3, 7, 2, 0).reverse.tail`
9. `List(4, 6, 9, 1, 8, 5, 3, 7, 2, 0).take(4).drop(2)`
10. `List(4, 6, 9, 1, 8, 5, 3, 7, 2, 0).take(4).take(2)`
11. `List(4, 6, 9, 1, 8, 5, 3, 7, 2, 0).drop(4).drop(2)`
12. `List(4, 6, 9, 1, 8, 5, 3, 7, 2, 0).drop(4).take(2)`
13. `List(List(1, 2, 3).length, List(4, 5).length, List(6, 7, 8, 9).length).product`

Opdracht 3 - String operaties
-----------------------------
In de les hebben we gekeken naar `Int`, `Boolean` en `List`. Om tekst te representeren, gebruiken we een
`String`. Je schrijft `"hello"` om een `String` te maken. Veel operaties die je op `List` kunt doen,
kun je ook op `String` doen.
Evalueer de volgende expressies over lijsten. Leg uit wat de expressie doet. Evalueer de expressie
vervolgens "uit je hoofd" en controleer daarna pas in Scastie of IntelliJ.
1. `"Hello world"`
2. `"Hello" + " " + "world"`
3. `"Hello".length`
4. `"".length`
5. `"Hello".head`
6. `"Hello".tail`
7. `"Hello".last`
8. `"Hello"(1)`
9. `"Hello".take(2)`
10. `"Hello".drop(3)`
11. `"world Hello".reverse`
12. Wat is het verschil tussen `"Hello".head` en `"Hello".take(1)`?
13. Wat is het verschil tussen `"".head` en `"".take(1)`?
14. Wat is het verschil tussen `"Hello"(1)` en `"Hello".drop(1).take(1)`?

Opdracht 4 - Vergelijken
------------------------
Als je wilt weten of 2 dingen gelijk zijn aan elkaar, gebruik je `==` (dubbele =). Bijv. `1 == 1`
geeft `true`, maar `1 == 2` is `false` en `"Hello hello".drop(1).take(4) == "Hello hello".drop(7)`
is `true`.
Wat is de waarde van de volgende expressies? Probeer het eerst uit je hoofd te doen en controleer
daarna pas in Scastie of IntelliJ.
1. `41 + 1 == 46 - 4`
2. `List(1, 2, 3).drop(1) == List(1, 2, 3).reverse.take(2).reverse`
3. `"Hello".take(2) == "Hello".reverse.drop(3).reverse`
4. `!(false || true) && (false || true) == !(false && true)`
5. `List(1, 2, 3, 4, 5).sum == List(3, 5).product`
6. `"Hello".head == "Hello".take(1)` (hint: zie opdracht 2.12)

Opdracht 5 - `last`
-------------------
De functie `last(xs)` geeft het laatste element uit de niet-lege lijst `xs`. Hieronder staan een
aantal mogelijke implementaties, waarvan sommige correct en andere incorrect zijn. Geef voor iedere
implementatie aan of deze correct is. Zo niet, leg uit waarom deze fout is.

1. `def last(xs: List[Int]): Int = xs.drop(xs.length - 1)`
2. `def last(xs: List[Int]): Int = xs.drop(xs.length - 1).head`
3. `def last(xs: List[Int]): Int = xs.reverse.tail`
4. `def last(xs: List[Int]): Int = xs.head.reverse`
5. `def last(xs: List[Int]): Int = xs(xs.length - 1)`
6. `def last(xs: List[Int]): Int = xs.drop(xs.length).head`
7. `def last(xs: List[Int]): Int = xs.reverse.head`
8. `def last(xs: List[Int]): Int = xs.reverse(xs.length - 1)`

Opdracht 6 - `init`
-------------------
De functie `init(xs)` geeft de niet-lege lijst `xs` terug zonder het laatste element. Hieronder
staan een aantal mogelijke implementaties, waarvan sommige correct en andere incorrect zijn. Geef
voor iedere implementatie aan of deze correct is. Zo niet, leg uit waarom deze fout is.
Probeer het eerst in je hoofd te doen en controleer dan met de REPL.

1. `def init(xs: List[Int]): List[Int] = xs.reverse.tail`
2. `def init(xs: List[Int]): List[Int] = xs.reverse.head.reverse`
3. `def init(xs: List[Int]): List[Int] = xs.tail.reverse`
4. `def init(xs: List[Int]): List[Int] = xs.take(xs.length)`
5. `def init(xs: List[Int]): List[Int] = xs.reverse.tail.reverse`
6. `def init(xs: List[Int]): List[Int] = xs.tail.take(xs.length - 1)`
7. `def init(xs: List[Int]): List[Int] = xs.drop(xs.length - 1)`

Opdracht 7 - `mkString`
-----------------------
Je kunt de inhoud van een `List` tonen als een `String` middels de functie `mkString`. Er zijn
hiervan 3 verschillende varianten. Zoek uit wat de verschillen tussen deze varianten zijn en leg dit
in je eigen woorden uit. Je kunt hiervoor gebruik maken van de [documentatie voor `List`].
Geef ook voorbeelden van hoe je de 3 varianten van `mkString` gebruikt. Betrek hierin zowel een
lijst met elementen (bijv. `List(1, 2, 3, 4, 5)` of `List(true, true, false, true, false, false)`)
als een lege lijst (`List()` of `List.empty`).

Opdracht 8 - Pythagoras
-----------------------
Schrijf een functie die, gegeven de lengte van de rechthoekszijden van een driehoek (a en b),
de lengte van de schuine zijde van de driehoek (c) uitrekent.

Maak hierbij geen gebruik van `math.hypot`!

```scala 3
def pythagoras(a: Double, b: Double): Double = ???
```

Merk op: in deze definitie gebruiken we voor de getallen geen `Int` (gehele getallen), maar
`Double` (kommagetallen). Bijv. `3` is een `Int`, maar `3.0` is een `Double`, net als `3.14159265`.
Kun je uitleggen waarom we hier `Double` gebruiken i.p.v. `Int`?

Test je functie met een paar voorbeelden.
* `pythagoras(3, 4)`
* `pythagoras(4, 3)`
* `pythagoras(7.3, 8.4)`
* `pythagoras(7, 24)`

Opdracht 9 - Oppervlakte en omtrek
----------------------------------
Implementeer twee functies die, gegeven de straal van een cirkel, respectievelijk de omtrek en
de oppervlakte van de cirkel berekenen. Test je functie met een paar voorbeelden.

```scala 3
def omtrek(straal: Double): Double = ???
def oppervlakte(straal: Double): Double = ???
```

[Scastie]: https://scastie.scala-lang.org/
[IntelliJ]: https://www.jetbrains.com/idea/
[documentatie voor `List`]: https://scala-lang.org/api/3.x/scala/collection/immutable/List.html
