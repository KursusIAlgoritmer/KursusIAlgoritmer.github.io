# Del 9 : Minimum spanning tree : MST

Spanning træ er Et udspændende træ...

## BFS & DFS
bredde først og dybde først er udspændte træer
(der er ingen cykler og alle knuder er forbundne)

-----------------------------------------------------------------------

### Vægtede kanter

Hvis kanterne har vægte - er "minimum spanning tree" den udspændte træ med den mindste vægt-sum

### Brute force : prøv alle - vælg mindste !

### Simplificering - vi antager alle vægte er forskellige
Konsekvens der er kun en MST!

-----------------------------------------------------------------------
***BEVIS***
## Def.: Et snit "A cut" er en opdeling af grafen i to indeholder
## Def. krydsende kant "crossing edge" er nogle der finder de to grupper

## Påstand: For et hvilket som helst snit er kanten med den mindste vægt med i MST...

## Bevis (mod-eksempel)
- Lad os antage at den mindste krydsende kant (e) ikke er med i MST ...
- Tilføjelse af e vil skabe en cykel!!
- Fjernelse af f (den tidligere krydsende kant) og tilføjelse af e vil give en MST men en mindre!
- Altså var den første MST ikke MST !!!

-----------------------------------------------------------------------

## Greedy MST algorithm - demo/skabelon
(Greedy : kigger kun på et lille del-problem og vælger lokalt det bedste ... finder ikke nødvendigvis den mest optimale løsning ...)
- start med alle grå
- find snit uden krydsende kanter - farv mindste vægtede kant sort
- gentaf indtil V-1 kanter er farvet sort

Dette er en demo/skabelon - det er endnu ikke præcist hvordan snittet vælges!!

-----------------------------------------------------------------------

***BEVIS***
## Påstand : The greedy algorithm finder MST

## Effektive implentaioner :  vælg snit, min-vægt
- Ex1: Kruskal algoritme (den snakker vi om)
- Ex2: Prims algoritme (den snakker vi om)
- Ex3: Brovkas algiritme

-----------------------------------------------------------------------

## Fjerner antagelse - alle kanter er ikke længere ens!

- der kan være flere MST, men algoritmen virker stadig

## Fjerner antagelse - grafen er fuldt forbundet

- finder mindste udspændte skov !!!!!

-----------------------------------------------------------------------

## Tilføjelse til API : laver en Edge klasse!
- either : returnerer v
- other(v) : returnerer w / other(w) : returnerer v
- compareTo

-----------------------------------------------------------------------

## MST API :
-edges
-weight
