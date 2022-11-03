## Obligatorisk aflevering 2 - deadline onsdag d19/10 eller mandag d.14/11

På en skibake ligger "n-1" nedadgående pister forbundet af "n" steder, der i nogle tilfælde forgrenner sig til nye pister. Ved ende-stationer, dvs. steder uden udgående forgreninger, er der mulighed for at tage en lift tilbage til bjergets top. Rejsetiden for hver pist er 1 minut. Rejsetiden for liften er altid 5 minutter.

## Del 1: Valgt løsningsmetode til appen
1. ***Oprettelse af kortet:*** Da alle pister er nedadgående vælges det at implementere piste-systemet som en rettet graf. For hver enkelt endestation, dvs. kanter med udgrad 0, tilføjes en yderligere forbindelse af fire nye knuder, der forbinder endestationen med toppen af bjerget. Denne forbindelse gør det ud for liften. Hvis hver kant svarer til en rejsetid på 1 minut, vil forbindelsen fra en endestation til toppen af bjerget dermed udgøre de beskrevne 5 minutter.     
2. ***Udskrivning af hurtigste vej:*** For at finde den hurtigste vej laves en bredde-først-søgning fra det ønskede startpunkt. Det er på den måde muligt at udskrive den hurtigste vej til et givent endepunkt, ved at udlade de ekstra fire lift-knuder.      
3. ***Beregning af hurtigste vej:*** For at finde tiden for den hurtigste rute laves en bredde-først-søgning fra det ønskede startpunkt. Antallet af kanter i ruten udgør dermed rejsetiden.   

### Del 2: Koden [https://github.com/KursusIAlgoritmer/KursusIAlgoritmer.github.io/tree/main/Aflevering2](https://github.com/KursusIAlgoritmer/KursusIAlgoritmer.github.io/tree/main/Aflevering2)

## Del 3: Analyse af udførselstiden som funktion af n
Den rettede graf er implementeret som en "adjacency list", og "oprettelsestiden" er derfor propertionel med E+V, hvor E er antallet af kanter og V er antallet af knuder. Operationerne "den hurtigste vej" og "den hurtigste tid" er implementeret som bredde-først-søgninger og udførselstiden for disse er altså ligeledes propertionelle med E+V.

Antallet af kanter, kaldet E, består af: (1) n-1 input, (2) 4 til liften og (3) mindst 1 og højest n-1, der forbinder endestationerne med liften:   
>E_max = 2n + 2   
>E_min = n + 4       

Antallet af knuder, kaldet V, vil altid bestå af inputtet n og 4 ekstra til liften:   
>V = n + 4       

Udførselstiderne, kaldet T, for "oprettelse af grafen", bergening af "den hustigste vej" og bergning af "den hurtigste tid" er altså i alle tilfælde:     
>Tmax = 3n+6    
>Tmin = 2n+8    
