# Rettet graf
kanterne har retning

----------------------------------------------

De samme problemstillinger kan laves med rettede grafer ...

----------------------------------------------

## Adjacency-list : her er de kun de kanter der går ud fra knuden ...
Forskellen fra ikke-rettet:
```java
//rettet
addEdge(int v, int w){
  adj[v].add(w);
}
//ikke-rettet
addEdge(int v, int w){
  adj[v].add(w);
  adj[w].add(v);
}
```

----------------------------------------------

## DFS er nøjagtigt den samme  for rettet-graf!!!!!!!

----------------------------------------------

## BFS er nøjagtigt den samme  for rettet-graf!!!!!!!

----------------------------------------------

## Applikationer
- programmer
- garbage collection

----------------------------------------------

## Topologisk sortering - 17.40 video 3

- Feks. "kursus afhængighed"

- DAG : Directed acylic graph
- DFS søgning...
- opretter først de besøgte knuder "post- order"
- retunerer alle knuder i omvendt rækkefølge "topologisk-order" : Dette kan løses med en stak

----------------------------------------------
Hvorfor virker det....
- første knude har "ud-grad" 0
- den næstsidste kan kun pege på den sidste
Bevis
-case1: Er allerede returneret
-case2:
-case3:

***Dette forstår jeg ikke så meget af!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!***

----------------------------------------------

DFS kan faktisk bruges til at finde en cykel ....

----------------------------------------------

Ting jeg også bør forstå:
- preorder
- postorder
- reverseorder
