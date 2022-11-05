komponenter# Kruskals algorithm

Den arbejder "grådigt"...

- sorterer kanter ift deres vægt
- tilføj næste kant hvis den ikke laver en cykel !

Ps: Når vi har valgt alle knuder er vi færdig!
----------------------------------------------------------------------------

## Correctness proof
Vi skal vise at valget af den næste kant i rækken svarer til at lave det mindste snit imellem to komponenter.

- vi antager at kruskals algoritme farver kanter sorte
- cut = settet af knuder forbundet til v i træet
- ingen krydsende kanter er sorte
- ingen af andre kanter er mindre - altså er den valgte kant den mindste

-----------------------------------------------------------------------------

Udfordring : hvordan bestemmer vi om der er en cykel ??

Union find .... kan anvendes

Hvis man laver en forbindelse imellem to forskellige komponeneter er der ingen cykel

Men hvis man laver en forbindelse imellem sammen komponent kommer der en cykel!

------------------------------------------------------------------------------

log*(n) : hvis n er antal kendte stjerner er reultatet 5

------------------------------------------------------------------------------

```java
public class KruskalMST{

  private Queue<Edge> mst = new Queue<Edge>();

  public KruskalMST(EdgeWeightedGraph G) {
    MinPQ<Edge> pq = new MinPQ<Edge>(G.edges());

    UF uf = new UF(G.V());

    while (!pq.isEmpty() && mst.size() < G.V()-1) {
      Edge e = pq.delMin();
      int v = e.either(), w = e.other(v);
      if (!uf.connected(v, w)) {
        uf.union(v, w);
        mst.enqueue(e);
      }
    }
  }
  public Iterable<Edge> edges()
  { return mst; }
}

```

------------------------------------------------------------------------------

## Påstand : Kruskals algoritme beregner MST i tid propertionalt  til E*logE i værste tilfælde

## Bevis:
- byg pq : 1 gang , E tid pr gang
- delete-min : E gange , logE tid pr gang
- union : V gange , log*V tid pr gang
- connected : E gange , log*V tid pr gang

E*log(E) er det tungeste skridt!!!!
