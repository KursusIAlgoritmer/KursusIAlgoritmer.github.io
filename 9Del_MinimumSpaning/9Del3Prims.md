# Prims Algoritme

 - starter med knude 0 og kigger på den mindste kant
 - Tilføj til T (tæet) mindtse kant der har et endpunkt i T
 - gentag indtil V-1 kanter

-----------------------------------------------------------------------------------------------

Opfundet flere gange : Jarnik 1930 , Djigstra 1957 , Prim 1959

-----------------------------------------------------------------------------------------------
Bevis for at den finder mst

Speiel case af greedy MST ...

- e , minimum vægt forbinder knude på træ med knude undefor træet
-  cut = set af knuder på træet
- ingen krydsende kanter er sort
- ingen har mindre vægt

-----------------------------------------------------------------------------------------------

 Udfordring : find den letteste af kanter der går ud fra træet

 Hvor svært???

- PQ med mindst et endepunkt i vores T
- Fjern minimum for at bestemme næste kant vi skal tilføje T
- Se bort fra kant hvis begge endpunkter er markerede (begge i T)
- Ellers.
- - Add kant til PQ hvis ene ende indeholder knuden i T
- - Add e til T og marker w  

-----------------------------------------------------------------------------------------------

Eksempel : Dovne , der bare smidder ubrugelige kanter (kanter der laver cykler) i PQ

1. starter med knude 0
2. smider alle kanter ind i PQ
3. fjern minimum kant,- og tilføjer den til T (og "tilføjer"/"flytter til" en ny knude)
4. smider alle kanter for den nye knude i PQ
5. gentag (4)

-----------------------------------------------------------------------------------------------
```java
public class LazyPrimMST {

  private boolean[] marked; // MST vertices
  private Queue<Edge> mst;  // MST edges
  private MinPQ<Edge> pq;   // PQ of edges

  public LazyPrimMST(WeightedGraph G) {
    pq = new MinPQ<Edge>();
    mst = new Queue<Edge>();
    marked = new boolean[G.V()];
    visit(G, 0);
    while (!pq.isEmpty() && mst.size() < G.V() - 1) {
      Edge e = pq.delMin();
      int v = e.either(), w = e.other(v);
      if (marked[v] && marked[w]) continue;
      mst.enqueue(e);
      if (!marked[v]) visit(G, v);
      if (!marked[w]) visit(G, w);
    }
  }

  private void visit(WeightedGraph G, int v) {
    marked[v] = true;
    for (Edge e : G.adj(v))
      if (!marked[e.other(v)])
        pq.insert(e);
  }

}
```

-----------------------------------------------------------------------------------------------

# UDFØRSELSTIDEN

Værste tilfælde : Beregner MST i tid propertonalt til E*logE og ekstra plads propertonalt til E

## Bevis:
- delete min : E gange , logE hver gang
- insert : E gange , logE hver gang

da E*logE er den dyreste (den eneste)

-----------------------------------------------------------------------------------------------

TID 1:10

-----------------------------------------------------------------------------------------------


# DEN IVRIGE VARIANT
Så længe der er mere end én kant ud til en knude, i prioitets-køen, er der for mange.
Der er kun nødvendigt med én.
...
Der er to hjælpe arrays- edgeTo[] og en distTo[]:

Dvs. proitetskøen indeholder elementer (v,edgeTo[],distTo[])

## Ny operation i prioitetskøen : inexed pririty queue
Det skal være muligt at ændre en nøgle, der hører til et bestemt index



- tilføjer knuder til prioriteteskø sorteret efter vægt  
