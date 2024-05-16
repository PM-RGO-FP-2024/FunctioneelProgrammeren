Week 1 - Introductie in Functioneel Programmeren en Scala
=========================================================
In deze les zullen we vooral kennis maken met Scala. Hiervoor beginnen we met wat rekenkundige
expressies en zien we een paar operaties die je met een lijst met getallen kunt doen. Vervolgens
kijken we naar wat logische operatoren en schrijven we een paar wiskundige functies.

Alle code-blokken in deze les zijn uitvoerbaar in Scala. Voer deze uit in je code editor om te zien
wat het resultaat is. Tijdens de les gebruiken we hiervoor [Scastie].
Als je thuis verder wilt met Scala of een eigen projectje wilt starten, raden we je aan om gebruik
te maken van [IntelliJ IDEA]. Zie ook de [handleiding] om Scala in IntelliJ te gebruiken.
Als je IntelliJ gebruikt voor de opdrachten bij deze lessen, kun je het beste een Scala Workbook maken.


Na deze les kun je:
-------------------
* een gegeven expressies evalueren in Scastie of een Scala Workbook
* voor eenvoudige expressies uitleggen waarom deze wel/niet voldoen aan een beschreven functionaliteit
* documentatie voor bestaande Scala functies terugvinden in de ScalaDocs
* eenvoudige functies implementeren m.b.v. de voorbeelden die in de les zijn besproken


Rekenkundige expressies
-----------------------
Net als bij wiskunde hebben we `+`, `-`, `*`, `/` en `%` om te rekenen met getallen. Daarnaast worden
haakjes gebruikt om aan te geven welke subexpressie eerst berekend moet worden.

```scala 3
1 + 1

2 + 3 * 4

(2 + 3) * 4
```

Als je een `/` doet op een geheel getal, dan komt daar ook een geheel getal uit: `10 / 5 = 2` en
`10 / 3 = 3`. Het restant van de deling krijg je met `%` (modulo): `10 % 5 = 0` en `10 % 3 = 1`.
Als je echter een `/` doet, maar ten minste één van de getallen is decimaal, dan komt er wel een
decimaal getal uit: `10 / 3.0 = 3.333...` en `10.0 / 3 = 3.333...`.

In de `math` package bevinden zich diverse andere rekenkundige tools die we kunnen gebruiken.
Zie hiervoor ook de [documentatie voor `math`].

```scala 3
math.pow(3, 2)

math.pow(3, 2) + math.pow(4, 2)

math.sqrt(math.pow(3, 2) + math.pow(4, 2))
```

We kunnen een expressie ook een naam geven, zodat we er later aan kunnen refereren. Middels het
`val` keywork maak je een **value** aan, die je vervolgens gelijk stelt (met de `=`) aan een expressie.

```scala 3
val a = 2 * 3
val b = 1 + 5

val c = a - b
```


Lijsten
-------
Als we meerdere getallen bij elkaar willen houden, stoppen we die in een **lijst** (bijv. een lijst
van je cijfers of de bedragen op een kassabon).

```scala 3
// een lijst maken
List(15, 6, 11, 0, 1, 8, 7)

// een lijst met de getallen van 1 t/m 5
1 to 5

// een lijst met de getallen van 1 tot 5
1 until 5

// twee manieren om een lege lijst te maken
List()
List.empty
```

Vervolgens kunnen we allerlei dingen met zo'n lijst doen.
```scala 3
// het eerste element van een lijst
List(1, 2, 3, 4, 5).head

// alles na het eerste element
List(1, 2, 3, 4, 5).tail

// het derde element uit de lijst (LET OP: een index begint bij 0!!!)
List(1, 2, 3, 4, 5)(2)

// de eerste drie elementen uit de lijst
List(1, 2, 3, 4, 5).take(3)

// alles na de eerste twee elementen uit de lijst
List(1, 2, 3, 4, 5).drop(2)

// de lengte van de lijst
List(1, 2, 3, 4, 5).length

// de som van alle elementen uit de lijst
List(1, 2, 3, 4, 5).sum

// het product (vermenigvuldiging) van alle elementen uit de lijst
List(1, 2, 3, 4, 5).product

// twee lijsten aan elkaar plakken tot één nieuwe lijst
List(1, 2, 3) ++ List(4, 5)

// de lijst in omgekeerde volgorde
List(1, 2, 3, 4, 5).reverse

// een representatie van de lijst als tekst, gescheiden door een komma en een spatie
List(1, 2, 3, 4).mkString(", ")
```


Logische operaties
------------------
Logische waarden (ook wel **Boolean**s genoemd) schrijf je in Scala als `true` en `false`. Hiermee geef
je aan dat iets 'waar' of 'niet waar' is. "_Er zitten 7 dagen in een week_" is een ware expressie,
dus `true`. "_Gras is rood_" is niet waar, dus `false`.

```scala 3
val zevenDagenInDeWeek = true
val grasIsRood = false
```

Met een `==` kun je twee dingen met elkaar vergelijken. Hieruit komt `true` als ze gelijk zijn en anders `false`.

```scala 3
1 + 1 == 3 - 1

4 == 5

List(1, 2, 3) == List(3, 2, 1).reverse
```

> **Let op:** de `=` gebruik je om een expressie aan een value te linken. Een `==` wordt gebruikt om te
vergelijken tussen twee expressies.

Met `!` kun je een `true` veranderen naar een `false` en omgekeerd. `!true` ("_not true_") is dus
gelijk aan `false` en `!false` ("_not false_") is gelijk aan `true`.

```scala 3
!true
!false

!grasIsRood
```

Met `!=` kun je vergelijken dat twee dingen _niet_ hetzelfde zijn

```scala 3
1 + 1 != 2

4 != 5

List(1, 2, 3) != List(4, 5, 6)
```

Met `&&` (AND) en `||` (OR) kun je twee logische expressies combineren.

```scala 3
true && true
true && false
false && true
false && false

true || true
true || false
false || true
false || false
```


Functies
--------
Functies kennen we uit de wiskunde: je stopt er iets (bijv. een getal) in en er komt iets (bijv.
een ander getal) uit. Bij de functie `f(x) = 2x + 5` is `f(0) = 5`, `f(2) = 9` en `f(-5) = -5`.

In Scala definiëren we een functie door te beginnen met `def`, gevolgd door de naam van de functie,
het argument tussen haakjes, een `=` en daarna de implementatie van de functie (wat de functie doet).

```scala 3
def f(x: Int) = 2 * x + 5

f(0)
f(2)
f(-5)

def dubbel(x: Int) = x + x

dubbel(2)
dubbel(3)
dubbel(4)

List(1, 2, 3, 4, 5, 6).take(dubbel(2))
```

Je kunt ook andere functies aanroepen in de implementatie van je functie

```scala 3
def viervoudig(x: Int) = dubbel(dubbel(x))

viervoudig(2)
viervoudig(3)
viervoudig(4)
```

Daarnaast kan een functie ook meerdere argumenten hebben

```scala 3
def som(a: Int, b: Int) = a + b
```


Opstapje naar volgende week
---------------------------
In de wiskunde is een functie beperkt tot getallen - dat is het enige wat je als input kunt geven
en het enige dat je als output kunt krijgen. In FP kun je ook andere types aan een functie meegeven
en als resultaat krijgen.

```scala 3
def faculteit(n: Int): Int = (1 to n).product
faculteit(5)

def gemiddelde(xs: List[Int]): Int = xs.sum / xs.length
gemiddelde(List(1, 2, 3, 4, 5))
gemiddelde(List(1, 2, 3, 4, 5, 6))

def isEven(x: Int): Boolean = x % 2 == 0
isEven(2)
isEven(3)
```


[Scastie]: https://scastie.scala-lang.org/
[IntelliJ IDEA]: https://www.jetbrains.com/idea/
[handleiding]: ../Tutorials/Install%20IntelliJ%20IDEA.md
[documentatie voor `math`]: https://scala-lang.org/api/3.x/scala/math.html
