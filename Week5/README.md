Week 5 - Recursie
=================
Met een for-comprehension itereren we over een lijst en transformeren ieder element uit de lijst
naar een andere waarde of kiezen we of een bepaald element wel of niet in de lijst blijft. Daarnaast
hebben we eerder gezien dat we kunnen pattern matchen over elementen om onderscheid te maken tussen
verschillende waarden en op basis daarvan te bepalen welke waarde teruggeven moet worden. In deze les
zullen we het itereren over lijsten en het concept van pattern matching gaan combineren om nog meer
functies op lijsten te kunnen definiëren. We maken hierbij gebruik van recursie - het splitsen van
een probleem in kleinere delen en het herhaaldelijk aanroepen van een functie vanuit die functie zelf.

Vanuit de wiskunde kennen we de faculteit ($n!$) als het product van alle getallen van $1$ t/m $n$.
In Scala kan dit in een functie `def faculteit(n: Int): Int` worden geïmplementeerd door precies die
omschrijving te gebruiken: neem de getallen `1 to n` en neem het product hiervan: `(1 to n).product`.
Zo is `faculteit(4)` geïmplementeerd als `(1 to 4).product`, wat zich vertaalt naar `4 * 3 * 2 * 1 = 24`.

Een andere definitie van faculteit is dat $n!$ ook gelijk aan $n \cdot (n - 1)!$, dus $n$ maal de
faculteit van het getal $n - 1$. In dit geval definiëren we $n!$ in termen van zichzelf: een faculteit
is gelijk aan een berekening waarin een kleinere faculteit betrokken is. Dit betekent ook dat er een
kleinste faculteit moet zijn waarvoor we een basis-waarde moeten definiëren. Anders zou deze herhaalde
operatie nooit eindigen en kan deze tweede definitie geen resultaat opleveren. In het geval van faculteit
is $0!$ de kleinste waarde en die stellen we gelijk aan `1`. Kortom: 

$$
n! =
\begin{cases}
1 & \text{if } n = 0 \\
n \cdot (n-1)! & \text{if } n > 0
\end{cases}
$$

Deze definitie van faculteit is direct te vertalen in Scala middels een pattern match op `n`:

```scala 3
def faculteit(getal: Int): Int = getal match {
  case 0 => 1
  case n => n * faculteit(n - 1)
}
```

Roepen we met deze nieuwe implementatie `faculteit(4)` aan, dan evalueert dat als volgt:

```text
faculteit(4)
==
4 * faculteit(3)
==
4 * 3 * faculteit(2)
==
4 * 3 * 2 * faculteit(1)
==
4 * 3 * 2 * 1 * faculteit(0)
==
4 * 3 * 2 * 1 * 1
==
24
```

In deze implementatie van `faculteit` wordt herhaaldelijk diezelfde functie `faculteit` aangeroepen
op een steeds kleinere input. Uiteindelijk komen we bij de kleinst mogelijke input uit, waarbij we de
herhaalde aanroepen (de recursie) stoppen en een basis-resultaat teruggeven.


Recursie
--------
Wanneer we problemen willen oplossen middels recursie is er altijd ten minste één simpel **basisgeval**
waarvoor we het antwoord kennen en ten minste één **algemeen geval** waarvoor we het probleem kunnen
verkleinen. In het voorbeeld van `faculteit(n)` hierboven is het basisgeval de `n = 0`, waarvoor bekend
is dat `faculteit(0) = 1`. Het algemene geval is `faculteit(n)`, waarvoor het probleem te verkleinen
is door `faculteit(n - 1)` te berekenen en dat te vermenigvuldigen met `n`.

Op zo'n zelfde manier kunnen we $a^b$ berekenen, oftewel $a$ vermenigvuldigd met zichzelf voor $b$ keren.
Uit de wiskunde weten we dat $a^0 = 1$ (het basisgeval) en dat $a^b$ gelijk is aan $a \cdot (a^{b-1})$
(het algemene geval).

De functie `pow(a: Int, b: Int): Int` kunnen we letterlijk vertalen vanuit de wiskunde naar Scala:

```scala 3
def pow(a: Int, b: Int): Int = b match {
  case 0 => 1
  case _ => a * pow(a, b - 1)
}
```

Voor het basisgeval waarbij `b = 0`, weten we dat daar altijd `1` uit komt, want $a^0 = 1$.
Voor het algemene geval vermenigvuldigen we `a` met `pow(a, b - 1)`, als in $a \cdot (a^{b-1})$.
Voorbeeld: voor `pow(2, 4)` worden de volgende stappen doorlopen:

```text
pow(2, 4)
==
2 * pow(2, 3)
==
2 * 2 * pow(2, 2)
==
2 * 2 * 2 * pow(2, 1)
==
2 * 2 * 2 * 2 * pow(2, 0)
==
2 * 2 * 2 * 2 * 1
==
16
```


`List` is recursief
-------------------
De `List` die in deze lessenserie al vaker aan bod is gekomen, is eigenlijk op dezelfde soort
recursieve manier opgebouwd. Het basisgeval voor een lijst is een _lege lijst_, een lijst waarin geen
elementen zitten. In Scala schrijven we een lege lijst als `Nil`. Het algemene geval is dat een lijst
niet leeg is en bestaat uit één waarde, gevolgd door een andere lijst: `A :: List[A]`.

De lijst van getallen 1 t/m 4 is dus eigenlijk het getal 1, gevolgd door een lijst van de getallen 2 t/m 4,
wat eigenlijk het getal 2 is, gevolgd door een lijst van de getallen 3 t/m 4, enz., eindigend met een
lege lijst: `1 :: 2 :: 3 :: 4 :: Nil`. In het algemene geval `A :: List[A]` noemen we het ene element
de _head_ van de list en de "andere lijst" wordt de _tail_ van de lijst genoemd.

Een lijst van elementen bestaat dus uit deze recursieve datastructuur. Deze kunnen we echter ook
gebruiken om een lijst stukje bij beetje af te breken. Als we de lengte van een lijst willen bepalen,
kunnen we dat doen met recursie en pattern matching. Voor het basisgeval dat een lege lijst (`Nil`)
weten we dat de lengte `0` is. In het algemene geval weten we dat de lijst bestaat uit een eerste
element (de _head_) en de rest van de lijst (de _tail_). De lengte van de lijst is dan 1 (voor de head)
plus de lengte van de tail.

```scala 3
def lengte[A](list: List[A]): Int = list match {
  case Nil => 0
  case _ :: tail => 1 + lengte(tail)
}
```

De lijst `List(4, 6, 3, 1)` kunnen we ook schrijven als `4 :: 6 :: 3 :: 1 :: Nil`. Als we de lengte
van deze lijst bepalen met de functie `lengte` hierboven, dan evalueert dat als volgt:

```text
lengte(4 :: 6 :: 3 :: 1 :: Nil)
==
1 + lengte(6 :: 3 :: 1 :: Nil)
==
1 + 1 + lengte(3 :: 1 :: Nil)
==
1 + 1 + 1 + lengte(1 :: Nil)
==
1 + 1 + 1 + 1 + lengte(Nil)
==
1 + 1 + 1 + 1 + 0
==
4
```

Op deze zelfde manier kunnen we voor een lijst met getallen de `som` functie definiëren. Opnieuw
onderscheiden we voor `List` de twee gevallen: een lege lijst `Nil` als basisgeval en een niet-lege
lijst `head :: tail`. De som van een lege lijst is gelijk aan `0` en de som van `head :: tail` is
gelijk aan `head` plus de som van `tail`.

```scala 3
def som(list: List[Int]): Int = list match {
  case Nil => 0
  case head :: tail => head + som(tail)
}
```

Met hetzelfde voorbeeld als hierboven evalueert `som(List(4, 6, 3, 1))` als volgt:

```text
som(4 :: 6 :: 3 :: 1 :: Nil)
==
4 + som(6 :: 3 :: 1 :: Nil)
==
4 + 6 + som(3 :: 1 :: Nil)
==
4 + 6 + 3 + som(1 :: Nil)
==
4 + 6 + 3 + 1 + som(Nil)
==
4 + 6 + 3 + 1 + 0
==
14
```

Van `som` is het een kleine stap naar `product`: de functie die alle getallen in een lijst met elkaar
vermenigvuldigt. Het product van een lege lijst stellen we gelijk aan `1` en het product van een
niet-lege lijst is gelijk aan de head vermenigvuldigd met het product van de tail.

```scala 3
def product(list: List[Int]): Int = list match {
  case Nil => 1
  case head :: tail => head * product(tail)
}
```

Opnieuw kunnen we als voorbeeld `product(List(4, 6, 3, 1))` evalueren:

```text
product(4 :: 6 :: 3 :: 1 :: Nil)
==
4 * product(6 :: 3 :: 1 :: Nil)
==
4 * 6 * product(3 :: 1 :: Nil)
==
4 * 6 * 3 * product(1 :: Nil)
==
4 * 6 * 3 * 1 * product(Nil)
==
4 * 6 * 3 * 1 * 1
==
72
```


Meerdere basisgevallen
----------------------
Tot nu toe hebben we gevallen gezien waarbij er slechts één basisgeval nodig is en één algemeen geval.
Het is echter ook mogelijk om meerdere basisgevallen en/of meerdere algemene gevallen te hebben.

Eerder in deze lessenserie zagen we hoe `List(1, 2, 3, 4).take(2)` de eerste twee elementen uit de
lijst neemt, wat resulteert in `List(1, 2)`. De functie `take(n)` is te implementeren middels recursie.
De lijst waaruit we een aantal elementen willen halen kan (net als in bovenstaande voorbeelden) leeg
of niet-leeg zijn. In het geval van een lege lijst, zijn er geen elementen om uit die lijst te halen
en wordt dus een lege lijst teruggegeven. Daarnaast moeten we ook rekening houden met de parameter `n`,
die zegt hoeveel elementen we uit de lijst willen halen. Wanneer `n <= 0`, willen we geen enkel element
uit de lijst halen en moet dus eveneens een lege lijst worden teruggegeven. In het geval
van een niet-lege lijst waarvoor `n > 0`, nemen we de head van die lijst en roepen we de functie `take`
recursief aan met de tail van de oorspronkelijke lijst. Omdat we nu de head van de lijst hebben meegenomen,
willen we nu nog maar `n - 1` elementen uit de tail halen.

```scala 3
def take[A](list: List[A], n: Int): List[A] = list match {
  case Nil => Nil
  case _ if n <= 0 => Nil
  case head :: tail => head :: take(tail, n - 1)
}
```

Wanneer `n` kleiner is dan de lengte van de lijst, zullen alleen de eerste `n` elementen worden
teruggegeven in het resultaat. In dit geval zal de recursie stoppen op het tweede basisgeval (`n <= 0`).

```text
take(List(4, 6, 3, 1), 2)
==
take(4 :: 6 :: 3 :: 1 :: Nil, 2)
==
4 :: take(6 :: 3 :: 1 :: Nil, 1)
==
4 :: 6 :: take(3 :: 1 :: Nil, 0)
==
4 :: 6 :: Nil
==
List(4, 6)
```

Wanneer `n` groter of gelijk is aan de lengte van de lijst, worden alle elementen van de lijst
teruggegeven. We krijgen dan natuurlijk minder elementen dan waar we om hebben gevraagd, maar meer
elementen zijn simpelweg niet terug te geven. In dit geval stopt de recursie op het eerste basisgeval
(`Nil`).

```text
take(List(4, 6, 3, 1), 5)
==
take(4 :: 6 :: 3 :: 1 :: Nil, 5)
==
4 :: take(6 :: 3 :: 1 :: Nil, 4)
==
4 :: 6 :: take(3 :: 1 :: Nil, 3)
==
4 :: 6 :: 3 :: take(1 :: Nil, 2)
==
4 :: 6 :: 3 :: 1 :: take(Nil, 1)
==
4 :: 6 :: 3 :: 1 :: Nil
==
List(4, 6, 3, 1)
```


Meerdere algemene gevallen
--------------------------
Met de kennis over itereren en for-comprehensions uit de vorige les kunnen we een functie `filterEven`
opstellen die uit een lijst van getallen uitsluitend de even getallen teruggeeft.

```scala 3
def filterEven(list: List[Int]): List[Int] = for {
  i <- list
  if i % 2 == 0
} yield i
```

Deze functie kunnen we echter ook implementeren middels recursie. Ook hier onderscheiden we weer
het geval dat de lijst leeg of niet-leeg is. Voor een lege lijst is er geen element om te filteren,
dus kan direct een lege lijst worden teruggegeven.

Een niet-lege lijst delen we zoals gebruikelijk op in de head en de tail. Wanneer de head een even
getal is, willen we deze in het uiteindelijke resultaat meenemen, terwijl wanneer de head een oneven
getal is, we dit element niet mee willen nemen in het resultaat. Hieruit volgen dus 2 algemene gevallen
die beide een recursieve stap maken:

```scala 3
def filterEven(lst: List[Int]): List[Int] = lst match {
  case Nil => Nil
  case head :: tail if head % 2 == 0 => head :: filterEven(tail)
  case _ :: tail => filterEven(tail)
}
```

Bij het evalueren van bijvoorbeeld `filterEven(List(4, 3, 6, 1))` zien we ook duidelijk deze twee
recursieve stappen gebruikt worden:

```text
filterEven(List(4, 3, 1, 6))
==
filterEven(4 :: 3 :: 1 :: 6 :: Nil)
==
4 :: filterEven(3 :: 1 :: 6 :: Nil)
==
4 :: filterEven(1 :: 6 :: Nil)
==
4 :: filterEven(6 :: Nil)
==
4 :: 6 :: filterEven(Nil)
==
4 :: 6 :: Nil
==
List(4, 6)
```
