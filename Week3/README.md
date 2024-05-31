Week 3 - Conditional expressions en pattern matching
====================================================
Een van de dingen die we in de afgelopen twee lessen zijn tegengekomen is het concept van logische
expressies, het type `Boolean` en de bijbehorende waarden `true` en `false`. We kunnen bijvoorbeeld
een functie definiëren die bepaalt of een `String` een palindroom of een isogram is (zie het huiswerk
bij les 1). We kunnen ook een functie definiëren die bepaalt of een jaartal een schrikkeljaar is.
Alledrie zijn dit voorbeelden van functies die een `Boolean` teruggeven.

```scala 3
def isPalindroom(s: String): Boolean = ???
def isIsogram(s: String): Boolean = ???
def isSchrikkeljaar(jaartal: Int): Boolean = ???
```

Ook hebben we expressies gezien die het type `Boolean` hebben, zoals `x >= 3`, `listA == listB`,
`string.isEmpty` of `x > 0 && x < 18`.


Conditionele expressies
-----------------------
We kunnen het resultaat van deze berekeningen, die `Booleans` dus, gebruiken om complexere functies
te maken. Dit doen we met **if-else** expressies.

```scala 3
// geeft de absolute waarde van een getal terug, |x|
// zie ook https://nl.wikipedia.org/wiki/Absolute_waarde
def abs(x: Int): Int = {
  if (x >= 0) x
  else -x
}

def beschrijfStringLengte(s: String): String = {
  if (s.isEmpty) "deze string is leeg"
  else s"deze string heeft lengte ${s.length}"
}
```

In de functie `abs` stellen we dat _**als** x groter is dan of gelijk is aan 0_, dat _**dan** `x`
teruggegeven moet worden_, en _**anders** `-x` moet worden teruggegeven_. Een if-else expressie
heeft dus 2 mogelijke paden die bewandeld kunnen worden, waarvan er uiteindelijk maar één wordt
gekozen op basis van de `Boolean` in de `if`-conditie.

Met het aanroepen van `abs(15)` gaan we dus eerst kijken of de **conditie** `true` of `false` is.
In dit geval dus `15 >= 0`, wat `true` oplevert. Daardoor kiezen we om de **if-branch** in te gaan
en dus `15` teruggeven. Bij `abs(-15)` bepalen we eerst of `-15 >= 0`. Dat is `false`, waardoor we
de **else-branch** in gaan en `-(-15)` of `15` teruggeven.

De functie `bepaalStringLengte` hierboven controleert eerst of een `String` leeg is (gelijk is aan `""`).
Als dat het geval is, wordt een ander resultaat teruggegeven dan wanneer de input niet leeg is.

Er kunnen ook opvolgende condities zijn als de eerste condities `false` bleken te zijn.

```scala 3
// bepaalt of een getal positief, negatief of nul is en geeft respectievelijk 1, -1 of 0 terug
// zie ook https://nl.wikipedia.org/wiki/Signum_(wiskunde)
def signum(x: Int): Int = {
  if (x > 0) 1
  else if (x < 0) -1
  else 0
}
```

In de functie `signum` onderzoeken we eerst of een getal positief is (de eerste `if`). Als dat niet
zo is, moeten we bepalen of het getal negatief is (de tweede `if`). Als ook dat niet het geval is,
komen we in een situatie waar het getal niet positief en niet negatief en dus 0 is (de `else`).

Je kunt ook meerdere condities hebben. In onderstaand voorbeeld wordt de score voor een toets vertaald
naar een beoordeling (de Amerikaanse variant voor een cijfer).

```scala 3
def grade(score: Int): String = {
  if (score >= 90) "A"
  else if (score >= 80) "B"
  else if (score >= 70) "C"
  else if (score >= 60) "D"
  else "F"
}
```

### Opmerking (1): volgorde van condities
In het `signum` voorbeeld kun je de expressies ook omdraaien: je kunt eerst kijken of `x < 0` en pas
daarna kijken of `x > 0`. In dit geval maakt die volgorde niet uit, omdat het een het ander uitsluit.

```scala 3
def signum(x: Int): Int = {
  if (x < 0) -1
  else if (x > 0) 1
  else 0
}
```

In het `grade` voorbeeld hierboven is het echter wel belangrijk dat de condities in deze volgorde staan!
Als je de eerste en tweede conditie zou omdraaien, zou niemand een `"A"` kunnen behalen.

### Opmerking (2): twee schrijfwijzen
Scala biedt vanaf versie 3 twee manieren om een if-else te schrijven. De manier zoals hierboven getoond
is de meest gangbare manier (en ook hoe het in eerdere versies werd beschreven) en is ook vergelijkbaar
met de meeste andere programmeertalen. Een alternatieve manier is om de if-conditie zonder haakjes te
schrijven. Om scheiding te maken tussen de conditie en de if-branch, wordt dan het keyword `then` gebruikt.
Je kunt deze schrijfwijze soms tegenkomen op internet, maar in deze lessenserie houden we vast aan
bovenstaande schrijfwijze.

```scala 3
def abs(x: Int): Int = {
  if x >= 0 then x
  else -x
}

def signum(x: Int): Int = {
  if x > 0 then 1
  else if x < 0 then -1
  else 0
}

def bepaalStringLengte(s: String): String = {
  if s.isEmpty then "deze string is leeg"
  else s"deze string heeft lengte ${s.length}"
}
```


Pattern matching
----------------
In plaats van if-else wordt in functioneel programmeren vaak gebruik gemaakt van **pattern matching**
(patroon herkenning). Hierbij proberen we een waarde te matchen tegen verschillende cases (waardes).
In de komende weken ga je meer zien van de kracht van pattern matching, maar in deze les beschouwen
we pattern matching als een alternatief voor if-else expressies.

```scala 3
def not(b: Boolean): Boolean = b match {
  case false => true
  case true => false
}
```

Het type `Boolean` heeft precies 2 waardes, en daarom heb je hierboven 2 cases nodig om alle opties
af te dekken. We noemen bovenstaande match **compleet**.

Wanneer een type meerdere (of zelfs oneindig veel) waardes heeft, kan een laatste `case _` gebruikt
worden om "alle andere gevallen" af te vangen.

```scala 3
def example(number: Int): String = number match {
  case 0 => "zero"
  case 1 => "one"
  case 2 => "two"
  case _ => "other"
}

example(0) // "zero"
example(1) // "one"
example(2) // "two"
example(5) // "other"
example(16) // "other"
example(-10) // "other"
```

Net als if-else expressies worden de cases in de match altijd van boven naar onder uitgevoerd.
Als je dus nog andere cases toevoegt na `case _`, zullen die nooit bereikt worden omdat `case _`
"_alle andere gevallen_" al afvangt.

Op diezelfde manier kun je ook tuples matchen.

```scala 3
def beschrijfCoordinaat(coord: (Int, Int)): String = coord match {
  case (0, 0) => "Oorsprong"
  case (x, 0) => s"$x op de x-as"
  case (0, y) => s"$y op de y-as"
  case (x, y) => s"Punt op ($x, $y)"
}

beschrijfCoordinaat((5, 3)) // "Punt op (5, 3)"
beschrijfCoordinaat((0, 0)) // "Oorsprong
beschrijfCoordinaat((0, 3)) // "3 op de y-as"
beschrijfCoordinaat((4, 0)) // "4 op de x-as"
```

Merk op dat we in dit voorbeeld `x` en `y` aan de waarde van één van de onderdelen van het tuple
binden. In het voorbeeld `(5, 3)` wordt `x = 5` en `y = 3`.

Met dit soort variabelen kunnen we pattern matching ook combineren met if-expressies.

```scala 3
def leeftijdsgroep(leeftijd: Int): String = leeftijd match {
  case l if l < 12 => "kind"
  case l if l < 18 => "jongere"
  case l if l >= 18 && l < 65 => "volwassene"
  case l if l >= 65 => "oudere"
}

leeftijdsgroep(18) // "volwassene"
leeftijdsgroep(36) // "volwassene"
leeftijdsgroep(70) // "oudere"
leeftijdsgroep(5) // "kind"
leeftijdsgroep(15) // "jongere"

def kwadrant(coordinaat: (Int, Int)): String = coordinaat match {
  case (0, 0) => "oorsprong"
  case (x, y) if x > 0 && y > 0 => "1e kwadrant"
  case (x, y) if x < 0 && y > 0 => "2e kwadrant"
  case (x, y) if x < 0 && y < 0 => "3e kwadrant"
  case (x, y) if x > 0 && y < 0 => "4e kwadrant"
  case (0, _) => "op de x-as"
  case (_, 0) => "op de y-as"
}
```


EXTRA - wat als een functie geen antwoord kan geven?
----------------------------------------------------
Als je een functie implementeert, kan het soms voorkomen dat de functie geen antwoord heeft voor
bepaalde input.

```scala 3
def gedeeldDoor(a: Double, b: Double): Double = a / b

def eersteElement[T](list: List[T]): T = list.head
```

De functie `gedeeldDoor` heeft geen antwoord wanneer `b == 0.0`; delen door 0 kan immers niet!
Ook de functie `eersteElement` heeft geen antwoord als de input lijst leeg is.

Om in dit soort gevallen toch een antwoord te kunnen geven, heeft Scala het type `Option[T]`. Als je
dit type teruggeeft in een functie, geef je eigenlijk aan dat de functie misschien een antwoord heeft
of misschien toch niet. Een `Option[T]` heeft twee waarden: `None` en `Some(t: T)`. De `None` geef
je terug als de functie geen antwoord heeft en als er wel een antwoord is, geef je die terug in een
`Some(...)`.

Vergelijk de implementaties van hierboven met de aangepaste implementaties hieronder, waarin het
`Option` type is gebruikt.

```scala 3
def gedeeldDoor(a: Double, b: Double): Option[Double] = {
  if (b == 0.0) None
  else Some(a / b)
}

def eersteElement[T](list: List[T]): Option[T] = {
  if (list.isEmpty) None
  else Some(list.head)
}
```

Voor lijsten is dit zo'n veel gebruikt patroon, dat `List` naar `head` ook een `headOption` heeft
om de functie `eersteElement` te implementeren.

```scala 3
def eersteElement[T](list: List[T]): Option[T] = list.headOption
```

Om verder te rekenen met een resultaat uit een functie die een `Option` teruggeeft, kun je gebruik
maken van pattern matching.

```scala 3
list.headOption match
  case None => ???
  case Some(value) => ???
```
