Week 0 - Waarom functioneel programmeren?
=========================================

In programmeren en het ontwikkelen van software, kunnen we een verdeling maken tussen 2 verschillende
stijlen van programmeren.

De procedurele stijl van programmeren focust op _hoe een bepaalde actie moet worden uitgevoerd_.
Je beschrijft dus de specifieke stappen die moeten worden doorlopen. Jij als programmeur bent daarbij
volledig in controle over wat er precies gebeurt.
In onderstaand voorbeeld zie je welke stappen er allemaal moeten worden genomen om een lijst met
getallen bij elkaar op te tellen.

```c
#include <stdio.h>

int main() {
    int numbers[] = {1, 2, 3, 4, 5};  // definieer een lijst met getallen
    int sum = 0;                      // begin de som bij 0
    for (int i = 0; i < 5; ++i) {     // loop over de indexes 0 tot 5
        sum += numbers[i];            // zoek het getal op de betreffende index op en tel dat op bij de som
    }
    printf("%d\n", sum);              // print de som
    return 0;                         // stop het programma
}
```

```python
numbers = [1, 2, 3, 4, 5]
total = 0
for number in numbers:
    total += number
print(total)
```

Aan de andere kant is er declaratief programmeren, waarbij de focus ligt op _het beschrijven van
het gewenste resultaat van de actie_ die moet worden uitgevoerd. De details van hoe dit precies moet
worden gedaan, laat je als programmeur daarbij over aan een onderliggend systeem.

```python
numbers = [1, 2, 3, 4, 5]
total = sum(numbers)
print(total)
```

```sql
SELECT SUM(value) as Total
FROM Numbers;
```

```scala 3
val numbers = List(1, 2, 3, 4, 5)
val total = numbers.sum
println(total)
```


Functioneel Programmeren
------------------------
Functioneel Programmeren past in die tweede categorie: het declaratief programmeren. In FP proberen
we een probleem op te knippen in kleinere deelproblemen die we vervolgens in wiskundige functies
proberen op te lossen. Vervolgens combineren we die functies om het oorspronkelijke probleem op te lossen.

In FP zijn _functies_ de belangrijkste bouwsteen. Functies doen één ding, namelijk het transformeren
van een input naar een output. Als je meerdere keren dezelfde functie gebruikt met dezelfde input,
zul je altijd dezelfde output terugkrijgen. Dit maakt dat je redelijk eenvoudig later kunt redeneren
over wat je functie zou hebben gedaan bij een bepaalde input.

Laten we als voorbeeld de functie `h(x) = 2x - 5` nemen. Deze transformeert een bepaalde waarde voor `x`
naar een bepaalde waarde voor `y`. Iedere keer dat je dezelfde waarde voor `x` invult, zal dezelfde
waarde voor `y` eruit komen.

Functies kun je ook samenstellen uit kleinere functies. Als je het probleem dat je met een bepaalde
functie probeert op te lossen, kunt opbreken in verschillende stappen, dan kun je voor iedere stap een
aparte functie maken en die later samenbrengen om je oorspronkelijke probleem op te lossen. Dit heeft
bijvoorbeeld als voordeel dat die kleinere functies vaak gemakkelijker te testen zijn dan één grote functie.

Het voorbeeld hierboven, `h(x) = 2x - 5` is eigenlijk al een samengestelde functie: je kunt deze opsplitsen
in een functie `f(x) = 2x` en een functie `g(x) = x - 5`. Je kunt dan ook schrijven `h(x) = g(f(x))`.
De functie `h` is dan de _compositie_ van `g` met `f`.

Dat FP een vorm van declaratief programmeren is, kun je mooi zien in onderstaand voorbeeld.
Als we een lijst van getallen gaan sorteren, dan doen we dat in FP met een paar simpele regels:
* als de lijst leeg is, hoeven we niets te sorteren en geven we een lege lijst terug.
* als de lijst één element bevat, dan is die al gesorteerd en kunnen we dat ene element teruggeven.
* anders heeft die lijst zowel een eerste element als "de rest van de lijst". De rest van de lijst
  verdelen we in twee nieuwe lijsten, namelijk de elementen die kleiner zijn dan het eerste element en 
  de elementen die groter zijn dan het eerste element. Beide lijsten sorteren we vervolgens weer en
  tot slot plakken we de kleinere (nu gesorteerde) elementen voor het eerste element en de grotere
  (nu gesorteerde) elementen erachter.

```haskell
quicksort [] = []
quicksort (x : []) = [x]
quicksort (x : xs) = quicksort smaller ++ [x] ++ quicksort larger
                     where
                       smaller = [a | a <- xs, a <= x]
                       larger = [b | b <- xs, b > x]
```

In dit voorbeeld zie je dat we focussen op _wat_ een gesorteerde lijst is (eerst de kleinere getallen,
dan het eerste getal en dan de grotere getallen) en niet op _hoe_ dat sorteren dan precies in z'n werk gaat.

We kunnen met een klein voorbeeld gemakkelijk zien hoe deze oplossing werkt.

```
  quicksort [3, 5, 1, 4, 2]
=
  quicksort [1, 2] ++ [3] ++ quicksort [5, 4]
=
  (quicksort [] ++ [1] ++ quicksort [2]) ++ [3] ++ (quicksort [4] ++ [5] ++ quicksort [])
=
  ([] ++ [1] ++ [2]) ++ [3] ++ ([4] ++ [5] ++ [])
=
  [1, 2] ++ [3] ++ [4, 5]
=
  [1, 2, 3, 4, 5]
```
