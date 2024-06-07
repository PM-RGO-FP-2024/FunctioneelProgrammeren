Week 4 - Itereren over collecties
=================================
Met een functie transformeren we een bepaalde waarde tot een andere waarde. Als je aan de functie
`def abs(x: Int): Int = if (x >= 0) x else -x` uit de vorige les een negatieve waarde geeft, dan
transformeert `abs` die in een positieve waarde en als je een positieve waarde meegeeft, dan wordt
deze getransformeerd naar zichzelf. Middels `def grade(score: Int): String` wordt een toets-score
naar een beoordeling (de Amerikaanse variant voor een cijfer, `A` t/m `F`).

In deze les breiden we dit principe verder uit: wat doen we als we een lijst getallen hebben, zoals
`List(4, -7, 2, 9, -6, -4)` en we willen ieder van die getallen transformeren naar zijn absolute
waarde? Of wat als we een `List[Int]` hebben en we willen die transformeren tot een `List[String]`
met de beoordeling voor iedere toetsscore. In dit soort gevallen willen we respectievelijk de functies
`abs` en `grade` toepassen op ieder element uit die lijst en dan een nieuwe lijst teruggeven.
We _itereren_ hiervoor door de lijst, passen voor ieder element in de lijst een functie toe en slaan
de resultaten van al die functie-aanroepen op in een nieuwe lijst.


`for`-comprehensions
--------------------
Scala's manier om te itereren is de _for-comprehension_.

Een for-comprehension in Scala ziet er als volgt uit:

```scala 3
val xs = List(1, 2, 3)
val result = for {
  x <- xs
} yield x + 1
```

Je kunt dit lezen als "_voor iedere `x` uit (`<-`) `xs`, bewaar (`yield`) `x + 1`_". Al die bewaarde
resultaten samen vormen de nieuwe lijst `result`. In het voorbeeld hierboven is `result = List(2, 3, 4)`.

Om de voorbeelden uit de introductie te gebruiken:

```scala 3
val getallen = List(4, -7, 2, 9, -6, -4)
val absoluteGetallen = for {
  getal <- getallen
} yield abs(getal)
// absoluteGetallen = List(4, 7, 2, 9, 6, 4)

val scores = List(65, 79, 91, 82, 54)
val grades = for {
  score <- scores
} yield grade(score)
// grades = List("D", "C", "A", "B", "F")
```

Op zo'n zelfde manier kun je, als je een lijst met persoonsgegevens hebt, deze transformeren naar
een lijst met alleen de naam.

```scala 3
case class Persoon(naam: String, leeftijd: Int, favorieteKleur: String)
val personen = List(
  Persoon("Anneke", 22, "rood"),
  Persoon("Jan-Willem", 18, "groen"),
  Persoon("Amy", 21, "blauw"),
  Persoon("Jordy", 17, "zwart"),
  Persoon("Menno", 12, "wit"),
)
val namen = for {
  persoon <- personen
} yield persoon.naam
```


Itereren over meerdere lijsten
------------------------------
Je kunt ook over meerdere lijsten tegelijk itereren.

```scala 3
for {
  x <- List(1, 2, 3)
  y <- List(4, 5)
} yield (x, y)
```

In bovenstaand voorbeeld itereren we door de lijst `List(1, 2, 3)` en voor ieder van die elementen
itereren we vervolgens door de lijst `List(4, 5)` om vervolgens alle combinaties `(x, y)` op te slaan.
Je itereert in dit voorbeeld dus 1x door `List(1, 2, 3)` en 3x door `List(4, 5)`. Het resultaat is:
`List( (1, 4), (1, 5), (2, 4), (2, 5), (3, 4), (3, 5) )`.

In de allereerste les hebben we al gezien dat je `List(1, 2, 3)` ook kunt schrijven als `1 to 3`.
Je kunt deze schrijfwijze ook gebruiken om een lijst te genereren die afhangt van een eerdere input.

```scala 3
for {
  x <- 1 to 3
  y <- x to 3
} yield (x, y)
```

In dit voorbeeld itereer je door de lijst `1 to 3` (dus `List(1, 2, 3)`) en voor ieder van die
elementen `x` genereer je een nieuwe lijst die bij `x` begint en tot `3` doorloopt. De eerste keer
(`x = 1`) is dat dus `List(1, 2, 3)`, de tweede keer (`x = 2`) is dat `List(2, 3)` en de derde keer
is dat `List(3)`. De tweede list in deze for-comprehension is dus telkens anders. Dat zie je ook terug
in het resultaat: `List( (1, 1), (1, 2), (1, 3), (2, 2), (2, 3), (3, 3) )`.

Een toepassing hiervan is de functie `concat[T](xss: List[List[T]]): List[T]`, die een lijst van lijsten
als argument neemt en alle lijsten aan elkaar plakt in één grote lijst. Dus,
`concat(List(List(1, 2, 3), List(4, 5, 6, 7), List(8, 9)))` geeft als resultaat `List(1, 2, 3, 4, 5, 6, 7, 8, 9)`.
De functie `concat` kun je implementeren door te itereren over de buitenste lijst. Ieder element in
die buitenste lijst is zelf een lijst en daardoor kun je dus ook over ieder element in de binnenste
lijsten itereren. Vervolgens verzamelen we al die individuele elementen in een nieuwe lijst, die het
resultaat van de functie vormt.

```scala 3
def concat[T](xss: List[List[T]]): List[T] = for {
  xs <- xss
  x <- xs
} yield x
```


Filteren in een lijst
---------------------
Tot nu toe hebben we gekeken naar transformaties op lijsten. Een andere nuttige toepassing van
itereren is om bepaalde elementen uit een lijst te verwijderen of juist in een lijst te behouden.
Dit filteren kunnen we met dezelfde for-comprehensions doen door een `if`-expressie toe te voegen.

Als we de lijst `List(4, -7, 2, 9, -6, -4)` uit de introductie van deze les gebruiken, maar uitsluitend
de positieve getallen eruit willen overhouden, dan schrijven we de for-comprehension als:

```scala 3
val getallen = List(4, -7, 2, 9, -6, -4)
val positieveGetallen = for {
  getal <- getallen
  if getal >= 0
} yield getal
```

Hierin itereren we dus door ieder `getal` in de lijst `getallen` en verzamelen alleen die getallen
in de resultaat-lijst die positief zijn.

Op zo'n zelfde manier kunnen we ook alleen de even getallen uit die lijst zoeken:

```scala 3
val evenGetallen = for {
  getal <- getallen
  if isEven(getal)
} yield getal
```

Je kunt ook meerdere if's gebruiken:

```scala 3
val positieveEvenGetallen = for {
  getal <- getallen
  if getal >= 0
  if isEven(getal)
} yield getal
```

In vervolg op het eerdere voorbeeld van de persoonsgegevens hierboven, kunnen we ook een for-comprehension
opstellen die alle twintigers vindt.

```scala 3
val twintigers = for {
  persoon <- personen
  if persoon.leeftijd >= 20 && persoon.leeftijd < 30
} yield persoon.naam
```

Je kunt deze filters in for-comprehensions ook gebruiken om te bepalen wat de factoren van een getal
zijn.

```scala 3
def factoren(n: Int) = for {
  x <- 1 to n
  if n % x == 0
} yield x

factoren(12) // [1, 2, 3, 4, 6, 12]
factoren(7) // [1, 7]
```

Deze functie kunnen we vervolgens gebruiken om te bepalen of een getal een priemgetal is. In dat geval
(zie `factoren(7)` hierboven) zijn de enige factoren `1` en het getal zelf.

```scala 3
def isPriem(n: Int) = factoren(n) == List(1, n)

isPriem(12) // false
isPriem(7) // true
```

Tot slot kunnen we nu een functie `priemgetallen` maken die alle priemgetallen onder een bepaalde
maximum waarde teruggeeft.

```scala 3
def priemgetallen(n: Int) = for {
  x <- 1 to n
  if isPriem(x)
} yield x

priemgetallen(40) // [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37]
```


Verschillende soorten collecties
--------------------------------
Als je het type van `List(true, false, true)` opvraagt, vind je dat dit `List[Boolean]` is.
Echter, als je het type van `1 to 3` opzoekt, zul je zien dat het type niet `List[Int]` is, maar dat
dit `Range` is. Er zijn in Scala meerdere soorten collecties, waarvan `List` en
`Range` er slechts 2 zijn. Een `List` bevat 0 of meerdere elementen van een willekeurig type.
Aan de andere kant betekent `Range` dan je een verzameling van opeenvolgende getallen (van type `Int`)
hebt.
Middels de `toList` methode kun je een `Range` transformeren naar een `List`:

```scala 3
(1 to 5).toList // List(1, 2, 3, 4, 5)
```

Wanneer het precieze type van de collectie niet uitmaakt (bijv. in het output-type van een functie),
dan kun je ook een `Seq` teruggeven (afkorting voor "sequence"). Zowel `List[T]` als `Range`
zijn `Seq[T]` (of `Seq[Int]` in het geval van `Range`), net als vele andere soorten collections.
In feite, de functies hierboven over factoren en priemgetallen gaven al geen `List` meer terug,
maar een ander `Seq` type!

![Collection diagram](Collections.svg)

Een ander collectie type is `Set[T]`, die net als `List[T]` 0 of meerdere elementen van het type `T`
bevat, maar `Set[T]` heeft de extra garantie dat de elementen uniek zijn. Waar `List(1, 2, 2, 3, 1)`
duplicaten bevat, zal `List(1, 2, 2, 3, 1).toSet` de duplicate elementen verwijderen: `Set(1, 2, 3)`.
Daarnaast is in een `Set` ook niet de volgorde gegarandeerd.

```scala 3
(1 to 5).toSet // Set(5, 1, 2, 3, 4)
```

Als je `(1 to 5).toList == List(2, 5, 1, 3, 4)` laat uitrekenen, dan levert dit `false` op, terwijl
`(1 to 5).toSet == Set(2, 5, 1, 3, 4)` wel `true` oplevert. Hoewel de `List` dezelfde getallen
bevat als de range, zijn de twee niet gelijk omdat ze in een andere volgorde staan. In de `Set`
variant is de volgorde onbelangrijk en daarom wordt alleen gekeken of de elementen hetzelfde zijn.

Als je een lijst van tuples hebt `List[(A, B)]`, kun je die omzetten naar een `Map[A, B]`. De `Map`
collectie is ideaal om snel te kunnen zoeken op een waarde van type `A` om het bijbehorende element
`B` te vinden. Let op dat ook als je van `List` naar `Map` gaat (middels `toMap`) de volgorde verloren
gaat en dat duplicate waarden voor `A` verloren gaan!

```scala 3
val list = List((1, "Jan"), (2, "Piet"), (3, "Joris"), (4, "Corneel"), (5, "Kees"))
val map = list.toMap
map.get(2)
```


EXTRA: `for`-comprehension over `Option[T]`
-------------------------------------------
In de vorige les hebben we gezien dat `Option[T]` aan kan geven dat het niet zeker is of een functie
een antwoord kan geven. Zo is `gedeeldDoor(a: Double, b: Double) = a / b` niet gedefinieerd wanneer
`b == 0.0`. Voor een `Option[T]` kun je òf een `None` teruggeven òf een `Some(...)`. Vervolgens kun
je hier ook een pattern match op doen om met het resultaat van een `Some(...)` of `None` verder te
werken in een volgende berekening. Zo'n pattern match kan handig zijn als je in de `Some(v)` case
een vervolgberekening wilt doen met de `v` én in de `None` case een alternatieve berekening wilt doen
of een andere waarde wilt gebruiken. Voor het geval dat je alleen maar wat met de `Some(v)` case wilt
doen en de `None` case onaangeraakt wilt laten, kun je ook gebruik maken van een for-comprehension.

Het `Option[T]` type kun je ook beschouwen als een `List[T]` met de extra restrictie dat `Option[T]`
uitsluitend 0 of 1 element heeft (resp. met `None` en `Some(v)`). Dat betekent dus dat je ook over
`Option[T]` kunt itereren middels een for-comprehension.

```scala 3
val list = List(5, 9, 4, 2, 1, 3)
val eersteElement = list.headOption
val result = for {
  i <- eersteElement
} yield i + 1
```

In bovenstaand voorbeeld nemen we het eerste element uit de lijst (mits de lijst niet leeg is) en
tellen nog `1` bij die waarde op. In het geval dat de lijst leeg zou zijn, zou `.headOption` een
`None` teruggeven en zou de for-comprehension niets doen en in plaats daarvan ook een `None`
teruggeven.

De for-comprehension biedt een mooie manier om functies samen te stellen die `Option` teruggeven.
In het voorbeeld hieronder nemen we eerst het eerste element uit de lijst en passen deze waarde
vervolgens toe op de functie `gedeeldDoor` uit de vorige les, die een `None` teruggeeft als de
noemer gelijk is aan `0.0`.
In dit geval is het eerste element een `5`, dus `list.headOption` levert op `Some(5)`. Aansluitend
levert `gedeeldDoor(20, 5)` het resultaat `Some(4)`. Van de `4` halen we nog `1` af, dus het resultaat
is `Some(3)`.
Had het eerste element in de lijst echter `0` geweest, dan had `list.headOption` het resultaat `Some(0)`
gegeven en `gedeeldDoor(20, 0)` had dan `None` geweest. In dat geval zou de `x - 1` niet zijn uitgevoerd
en had het eindresultaat ook `None` geweest.
Ditzelfde geldt voor het geval dat de `list` leeg was geweest. Dan had `list.headOption` geresulteerd
in een `None` en was ook de `gedeeldDoor` niet uitgevoerd!

```scala 3
val list = List(5, 9, 4, 2, 1, 3)
for {
  i <- list.headOption
  x <- gedeeldDoor(20, i)
} yield x - 1
```
