Introductie in Functioneel Programmeren
=======================================

Functioneel Programmeren (FP) is een manier van programmeren waarbij functies de belangrijkste bouwstenen zijn.
Functies kennen we uit de wiskunde zoals `f(x) = 2x - 5`, die ieder getal in `x` transformeert tot een
(ander) getal in `y` en waar iedere keer dat je dezelfde `x` in `f(x)` stopt, hetzelfde resultaat eruit komt.
Je kunt verschillende functies ook samenstellen, door bijv. het resultaat van `f(x)` als input te geven voor
een andere functie `g(x)`, die dus eigenlijk voortbouwt op het resultaat van `f(x)` zonder dat we `f` hiervoor
hoeven aan te passen.

Datzelfde doen we in FP, waarin we software maken die is opgebouwd en samengesteld uit verschillende kleine functies.
Door op deze manier onze programma's te schrijven, krijg je code die goed begrijpbaar is voor jezelf en anderen
die meewerken aan een project. Kleine functies zorgen er ook voor dat je code eenvoudig te testen is, dat je er
gemakkelijk over kunt redeneren waardoor je snel kunt bepalen wat er in bijzondere situaties gebeurt. Ook maakt
deze manier van programmeren het eenvoudig om je programma's te parallelliseren, waardoor je meerdere taken
tegelijkertijd kunt draaien en dus sneller tot een oplossing komt.

Wat gaan we in de komende weken doen?
-------------------------------------
In de lessen ga je kennismaken met een aantal concepten uit FP. Om die goed te kunnen begrijpen is het belangrijk
om hier veel mee te oefenen. Daarom zal een groot deel van de lestijd gereserveerd zijn voor practica, waarin we
door het oplossen van verschillende problemen ervaring opdoen met programmeren in een functionele manier. Je werkt
hieraan in tweetallen (pair-programming). De opdrachten die tijdens de les niet af zijn, zijn huiswerk.

In deze lessenserie gebruiken we de programmeertaal [Scala]. Deze taal heeft goede ondersteuning in vrijwel alle
code editors en IDE's. Helaas kunnen we die niet op de laptops van school installeren en daarom gebruiken we de
online Scala editor [Scastie]. Zie ook een [korte demo van Scastie] om hiermee aan de slag te gaan.
Als je op je eigen computer verder wilt gaan, of zelf een project wilt beginnen met Scala, adviseren we om [IntelliJ IDEA]
te gebruiken. Zie ook de [handleiding om IntelliJ te installeren] in deze repository.

De volgende onderwerpen (per week) zullen aan de orde komen:
* [Week 0 - Waarom functioneel programmeren?](/Week0) (26 april 2024)
* Week 1 - Introductie in Scala en functioneel programmeren (17 mei 2024)
* Week 2 - Functies en types (24 mei 2024)
* Week 3 - Conditionele expressions en pattern matching (31 mei 2024)
* Week 4 - List comprehensions (7 juni 2024)
* Week 5 - Recursie (14 juni 2024)
* Week 6 - Software ontwikkeling bij Voogd&Voogd (21 juni 2024)

De oplossingen van de practica lever je als tweetal in.
* De deadline voor het inleveren van de oplossingen van de vorige les is telkens de dag van de volgende les om 9:00 uur.
  Dus het practicum voor Week 1 lever je uiterlijk in op de dag dat de les van Week 2 wordt gehouden.
* Inleveren van de oplossingen doe je in PDF-formaat als bijlage van een e-mail. Kopieer telkens je oplossing
  vanuit Scastie of IntelliJ naar een Word/GoogleDoc document en exporteer dat na afloop naar PDF.
* De e-mail met de oplossingen stuur je naar zowel de gastdocent als beide informatica-docenten.
  E-mailadressen worden in de eerste les uitgedeeld.

Heb je vragen over de lessen of de practica, stel ze dan in de [GitHub Discussions]. Zie ook de
[handleiding voor Discussions].

[Scala]: https://www.scala-lang.org/
[Scastie]: https://scastie.scala-lang.org/
[korte demo van Scastie]: Tutorials/Run%20Scastie.md
[IntelliJ IDEA]: https://www.jetbrains.com/idea/
[handleiding om IntelliJ te installeren]: Tutorials/Install%20IntelliJ%20IDEA.md
[GitHub Discussions]: https://github.com/PM-RGO-FP-2024/FunctioneelProgrammeren/discussions
[handleiding voor Discussions]: Tutorials/GitHub%20discussion.md
