# Shortest Paths
Video 1:27    

Hvad skal vi kunne finde ud af
- single sorce : fra s til en anden    
- single sink : fra alle til en bestemt t    
- source-sink: fra s til t    
- all pairs : imellem alle  

## restrictions :
ikke-negative vægte, euclidiske vægte (afstande ikke vilkårlige), tilfældige vægte

## cykler :
ingen directed cykler ...?
ingen negative cykler

Antagelse: Der eksiterer en vej fra s til v !!!!!!!!!!!!!!!!!!!!!!!!!

------------------------------------------------------------------------
# Hvilken API
Rettet graf!

------------------------------------------------------------------------
# Single source...

Mulig klient-kode
```java
SP sp = new SP(G, s);
for (int v = 0; v < G.V(); v++) {
  StdOut.printf("%d to %d (%.2f): ", s, v, sp.distTo(v));
  for (DirectedEdge e : sp.pathTo(v))
    StdOut.print(e + " ");
  StdOut.println();
}
```

Man kan anvende en korteste træ SPT (shortest path tree):

repræsenteret af til vertex indexed arrays
- edgeTo[] (edge objektet)
- distTo[] (samlet vej)

```java
public double distTo(int v)
{ return distTo[v]; }
public Iterable<DirectedEdge> pathTo(int v) {
Stack<DirectedEdge> path = new Stack<DirectedEdge>();
for (DirectedEdge e = edgeTo[v]; e != null; e = edgeTo[e.from()])
path.push(e);
return path;
}
```
-------------------------------------------------------------------------------

# RELAX EDGE ::::  e =  v->w

- distTo[v] ogd distTo[w]  er længden af den korteste kendte vej fra s til v
- distTo[w] er sidste kant på den korteste kendte vej fra s til w
- HVIS e = v->w giver en kortere vej til w... opdater da både distTo[w] og edgeTo[w]



v -> w <-
```java
//Vi spørger om denne vej/kant giver en kortere længde...
private void relax(DirectedEdge e) {
  int v = e.from();
  int w = e.to();
  if (distTo[w] > distTo[v] + e.weight()) {
    distTo[w] = distTo[v] + e.weight();
    edgeTo[w] = e;
  }
}
```
---------------------------------------------------------------------------------
Den eneste måde vi opdaterer vores "edgeTo" og "distTo" er via vore "relax"

Når vi har fundet den hurtigste vej - gælder:
- distTo[s] = 0
- For hver knude v er distTo[v] længden fra s til v
- For hver edge e = v -> w, distT[w] <= distT[v] + e.weight()

---------------------------------------------------------------------------------

Generel algoritme
- sæt distTo[0] = 0
- sæt distTo[v] = uendeligt (alle andre)
- gentag indtil optimum fundet : relax hver kant !!!!!!

---------------------------------------------------------------------------------
 Beregner altid SPT fra s


Fordi:
- distTo[v] er altid en længde på en simpel vej fra s til v
- alle succesfulde relax formindsker distTo[v] for en given v ...
- distTo[v] kan formindskes et begrænset antal gange ....

Vejen går ikke gennem den samme knude mere end 1 gang!

---------------------------------------------------------------------------------
# SPT algoritmer
# Der er tre måder/strategier for at kalde relax...

- Dijkstra (ikke negative vægte)
- Toplogisk sort (ingen rettede cykler)
- Bellman-Ford (ingen negative cykler)

---------------------------------------------------------------------------------
---------------------------------------------------------------------------------
---------------------------------------------------------------------------------

Digstras algoritme -
- starter med knude s
- kalder vi relax på alle rudgående kanter
(nu er vi færdige med knude 0)
- vælger den knude der har den "korteste-vej" knude
- kalder igen relax på denne knude
- vælger igen knude der har den "korteste-vej" knude

Når vi har været igennem alle knuder er vi færdige

---------------------------------------------------------------------------------

Digstras algoritme beregner SPT i alle vægtede-grafer med ikke-negative vægte

Bevis:
- kant v->w er relaxed kun en gang ( når knude v er relaxed ), hvilket efterlader distTo[w] <= distTo[v] + e.weight()
- uligheden holder helt indtil færdig.... FORDI: distTo[w] kan ikke stige!! og distTo[v] kan ikke ændre sig
- så derfor holder ...

---------------------------------------------------------------------------------
Der er selvfølgelig optimeringer hvor vi kun behøver kigge på delmængder af grafen...

---------------------------------------------------------------------------------
Prims algoritme er esssentielt set den samme algoritme

- begge algoritmer finder et udspændt træ
- Hoved forskel :
- prim anvender nærmeste vertex i træet
- Dijkstra anvender nærmeste vertex fra "kilden" (det sted man er nået til)

---------------------------------------------------------------------------------
Fire af vores graf-søgnings algoritmer er den samme
- vedligehold et sæt af undersøgte knuder S
- Udbyg S med eksakt et endepunkt i S

- DFS: tager kanter fra en knude der er besøgt senest
- BFS: tager kanter fra en knude der er besøgt først
- Prim : tager kant der har mindst vægt
- Dijkstra : tager kant til knude der er tættest på ?? (fra kilden)

---------------------------------------------------------------------------------
---------------------------------------------------------------------------------
---------------------------------------------------------------------------------

# Vi kan gøre det hurtigere hvis der er INGEN RETTEDE CYKLER

Toplogisk søgning! (kan med vores dybde søgning... DFS )

Gennemløber dem i denne rækkefølge og kalder relax på alle udgående kanter

---------------------------------------------------------------------------------

## Content aware resize

Fjerner mindst synlige "korteste vej" fra top til bund - ved resize vertikalt...


---------------------------------------------------------------------------------
---------------------------------------------------------------------------------
---------------------------------------------------------------------------------

# Negative vægt

Korrektheds beviset for Dijkstra er det et krav, at der ikke er negative vægte

Kan ikke fikses ved at lægge en konstant til...

---------------------------------------------------------------------------------

# Ny algoritme - der håndterer negative kanter
# Bellman ford

negative kanter - men ikke negative cykler (ellers cykler man bare rundt til man har minus uendeligt)

```java
for (int i = 0; i < G.V(); i++)
for (int v = 0; v < G.V(); v++)
for (DirectedEdge e : G.adj(v))
relax(e);
```

man kan stoppe iterationen efter pass2 hvis der ikke er nogen ændringer

---------------------------------------------------------------------------------
## Praktisk forbedring

- Observation : hvis distTo[v] ikke ændrer sig igennem et pass så behøves der ikke relax af nogen kanter fra v i næste pass

- Løsning: hav en kø med de kanter der ændrer sig ...

algorithm | restriction | typical case | worst case | extra space
SE SLIDES...
topological sort no directed cycles E + V E + V V

- directed cycles = harder
- negative weights = problem harder
- negative cykler = umuligt

---------------------------------------------------------------------------------
---------------------------------------------------------------------------------
---------------------------------------------------------------------------------
# FIND NEGATIVE CYKLER
Hvis Bellman-Ford ændrer en vertex i det pass V er der en negativ cykel -
og edgeTo kan finde stedet!

---------------------------------------------------------------------------------
negative cycle application - arbitrage detection
