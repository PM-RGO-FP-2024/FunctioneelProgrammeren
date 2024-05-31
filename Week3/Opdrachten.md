Practicum - Week 3
==================
Dit practicum hoort bij de les "_Conditional expressions en pattern matching_".
Om onderstaande opdrachten uit te voeren, kun je gebruik maken van [Scastie] of een Scala Worksheet
als je bijv. [IntelliJ] hebt geïnstalleerd op je eigen laptop.

**Deadline:** uiterlijk vrijdagmorgen 7 juni 2024 9:00 uur per mail inleveren bij de 3 docenten

Opdracht 0 - Booleaanse combinaties
-----------------------------------
Hieronder staan een aantal omschrijvingen van functies over type `Boolean`. Maak steeds een functie
definitie die past bij deze omschrijving en geef de juiste implementatie. Gebruik hierbij if-else
structuren. Maak in deze implementaties GEEN gebruik van `||`, `&&`, `!` en `^`. Test steeds iedere
functie tegen alle mogelijke combinaties van input.

1. De functie `not` neemt 1 waarde van type `Boolean` en geeft `true` terug als deze waarde `false`
   is en `false` als deze waarde `true` is
2. De functie `or` neemt 2 waarden van type `Boolean` en geeft `true` terug als ten minste één van
   deze 2 waarden `true` is.
3. De functie `and` neemt 2 waarden van type `Boolean` en geeft uitsluitend `true` terug wanneer
   beide waarden `true` zijn.
4. De functie `xor` neemt 2 waarden van type `Boolean` en geeft uitsluitend `true` terug wanneer
   één van beide waarden `true` is.

Opdracht 1 - FizzBuzz
---------------------
Implementeer de functie `def fizzBuzz(i: Int): String` die voldoet aan de volgende regels:
1. als het getal `i` deelbaar is door 3, geef `"Fizz"` terug
2. als het getal `i` deelbaar is door 5, geef `"Buzz"` terug
3. als het getal `i` deelbaar is door zowel 3 als 5, geef `"FizzBuzz"` terug
4. anders, geef het getal terug als een `String` (gebruik `i.toString()`)

Test je implementatie door verschillende getallen uit te proberen.
Hint: om te bepalen of een getal `i` deelbaar is door een ander getal `n`, gebruik je `i % n == 0`

Opdracht 2 - Booleaanse combinaties (opnieuw)
---------------------------------------------
Implementeer de functies uit opdracht 0 nogmaals, maar nu met pattern matching in plaats van if-else.
Test dat deze tweede implementatie dezelfde resultaten heeft als de eerste implementatie.

Opdracht 3 - Eerste element in de lijst is even
-----------------------------------------------
Maak een functie die een lijst van getallen inneemt en bepaalt of het eerste getal in de lijst
een even getal is. Implementeer deze functie met een if-else expressie. De functie moet aan het
volgende voldoen:
1. als de lijst leeg is, moet de functie `"deze lijst is leeg"` teruggeven
2. als het eerste element even is, moet de functie `"het eerste getal is even"` teruggeven
3. als het eerste element oneven is, moet de functie `"het eerste getal is oneven"` teruggeven

Leg vervolgens uit in hoeverre de volgorde van de if's in deze functie belangrijk zijn. Kun je de volgorde
ook veranderen zonder het gedrag van de functie te veranderen? Kun je de voorwaarden hierboven ook in
een andere volgorde controleren?

Opdracht 4 - De naam van de maand
---------------------------------
Schrijf een functie die, gegeven het getal van een maand, de naam van die maand teruggeeft.
Bijv. `maandNaam(5)` geeft `"mei"` terug en `maandNaam(8)` geeft `"augustus"`.
Test je resultaat door verschillende getallen in je functie te stoppen.
Kies zelf of je hiervoor een if-else of pattern matching gebruikt. Licht toe waarom je de voorkeur
geeft aan de ene of de andere variant.

Opdracht 5 - Aantal dagen in de maand
-------------------------------------
Maak een functie die het aantal dagen in een maand geeft.
`def aantalDagenInEenMaand(maand: Int, jaar: Int): Int`
Let op: februari heeft alleen 29 dagen in een schrikkeljaar! Houd daar rekening mee in het ontwerp
van je functie. Gebruik de functie `isSchrikkeljaar` uit de opdrachten van vorige week of maak een
nieuwe implementatie met een if-else expressie.

Opdracht 6 - Datumvalidatie
---------------------------
In deze opdracht ga je een functie implementeren die valideert of een datum geldig is.
`def valideerDatum(dag: Int, maand: Int, jaar: Int): String`
Gebruik de functies die je in opdracht 4 en 5 hebt gemaakt om de naam van een maand te schrijven
en te valideren of het dag-nummer geldig is voor de gegeven maand en het gegeven jaar.
Hieronder staan de voorwaarden waar de functie aan moet voldoen. Laat in je uitwerking ook zien dat
je met deze (en/of andere) voorbeelden hebt getest.

* Als de ingegeven maand te klein is, geeft de functie een foutmelding terug
    * `valideerDatum(12, -5, 2024)` geeft terug `"Ongeldige maand -5; maand moet >= 1"`
* Als de ingegeven maand te groot is, geeft de functie een foutmelding terug
    * `valideerDatum(12, 15, 2024)` geeft terug `"Ongeldige maand 15; maand moet <= 12"`
* Als de ingegeven dag te klein is, geeft de functie een foutmelding terug
    * `valideerDatum(-3, 5, 2024)` geeft terug `"Ongeldige dag -3; dag moet >= 1"`
* Als de ingegeven dag te groot is voor de gegeven maand/jaar, geeft de functie een foutmelding terug
    * `valideerDatum(29, 2, 2023)` geeft terug `"Ongeldige dag 29; in februari 2023 moet dag <= 28"`
    * `valideerDatum(32, 5, 2024)` geeft terug `"Ongeldige dag 32; in mei 2024 moet dag <= 31"`
* Als de datum geldig is, geeft deze functie de datum terug
    * `valideerDatum(27, 5, 2024)` geeft terug `"27 mei 2024"`
    * `valideerDatum(29, 2, 2024)` geeft terug `"29 februari 2024"`
    * `valideerDatum(31, 7, 1992)` geeft terug `"31 juli 1992"`

EXTRA - Opdracht 7 - Weekdag
----------------------------
Je kunt uitrekenen op welke dag van de week een gegeven datum valt. In [deze blog] staat beschreven
hoe je dat moet doen. Implementeer de functie `def weekdag(dag: Int, maand: Int, jaar: Int): String`.
Je mag aannemen dat er alleen geldige datums in deze functie worden ingegeven.

EXTRA - Opdracht 8 - Options
----------------------------
Naast `headOption` heeft de `List` nog andere functies die een `Option[T]` teruggeven. Lees door de
[documentatie van Scala's List], kies een paar functies met `Option[T]` en maak zelf een paar voorbeelden
waarin je deze functies gebruikt.

EXTRA - Opdracht 9 - Options
----------------------------
Implementeer de functie `eersteStringHeeftEvenLengte` hieronder door gebruik te maken van `headOption`
en pattern matching. De functie moet voldoen aan het volgende:
* wanneer de lijst leeg is, wordt `"de gegeven lijst is leeg"` teruggegeven
* wanneer het eerste element in de lijst een even lengte heeft, wordt `"de eerste String in deze lijst heeft een even lengte"` teruggegeven
* wanneer het eerste element in de lijst een oneven lengte heeft, wordt `"de eerste String in deze lijst heeft een oneven lengte"` teruggegeven

```scala 3
def eersteStringHeeftEvenLengte(list: List[String]): String = ???
```

[Scastie]: https://scastie.scala-lang.org/
[IntelliJ]: https://www.jetbrains.com/idea/
[deze blog]: https://artofmemory.com/blog/how-to-calculate-the-day-of-the-week/
[documentatie van Scala's List]: https://www.scala-lang.org/api/current/scala/collection/immutable/List.html
