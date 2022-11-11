# 7 Del - Grafer

>Def:
>>Et antal *knuder* og et antal *kanter*

Man kan repræsentere alle mulige ting ....

- knude : vertex
- kanter : edge
- sti : path
- cykel : cycle
- knude-grad : antal tilhørende kanter

## Problemer
- er der en veh fra s til t
- korteste vej
- er der en cykel
- osv.

-------------------------------------------------------------------------

## Ikke rettet graf - Undirected graph

Anomali :
- Der kan være "self loop"
- Der kan være "paralelle kanter"

-------------------------------------------------------------------------

## API
- Graf(int V)
- addEdge(int v, int w) : fra v til w
- Iterable<Integer> adj(int v) : kanter tilhørende v
- V() : antal knuder
- E() : antal kanter

-------------------------------------------------------------------------

## Implementation

### list of edges - linked list or array
>Hvor længe tager der at finde alle "kanter" til "v"...
>>Så skal man løbe hele listen igennem... altså V tid....

### ajacency matrix
Så vil der være redundans ...
kanten fra 2 til 1 vil resultere i at:      
list[2][1]=1 og list[1][2]=1
>>Koster igen V tid....

### Adjacency list - vertex-indexed array of linked-lists (kunne være en anden implentation af "bag")
Oftest anvendte :   
Igen er der noget redundans   
>>Koster denne gang kun det antal kanter der ligger i den linked-list

Hvis en graf er meget "dense" kan der måske være en fordel at bruge en matrix ...
Men ellers er grafen oftest "sparse"

 -----------------------------------------------------------------------

 | repræsentation          | plads  | insæt kant                        | Kanter v til w? | antal kanter på v?  |
 |-------------------------|------ -|-----------------------------------|-----------------|---------------------|
 | list of edges           | E      | 1                                 | E               | E                   |
 | adjacency matrix        | V^2    | 1 (paralelle ikke muligt)         | 1               | V                   |
 | adjacency list          | E+V    | 1                                 | grad(v)         | grad(v)                   |

*** HER ER EN FEJL : plads i den sidste = E + 2*V
  -----------------------------------------------------------------------
### IMPLEMENTATION

```java
public class Graph {
private final int V;
private Bag<Integer>[] adj;
public Graph(int V) {
this.V = V;
adj = (Bag<Integer>[]) new Bag[V];
for (int v = 0; v < V; v++)
adj[v] = new Bag<Integer>();
}
public void addEdge(int v, int w) {
adj[v].add(w);
adj[w].add(v);
}
public Iterable<Integer> adj(int v)
{ return adj[v]; }
}
```
