# Binær search tree

## En speciel datastruktur - hvis formål er at kunne søge nemmere
Det er opbygget som en binær-søgning   

Det er udbygning af linked-list, hvor hvert node har to links til to nye.   
- Alle "left" elemeneter er mindre   
- Alle "højre" elementer er størrer   

--------------------------------------------------------------------------------

## Implementation
- konstruktør : Node(Key k, Value v)  
- og put, get, delete, iterator

--------------------------------------------------------------------------------
## unsuccesfuld/succesfuld search
- hvis den er un-succes rammer vi en tom plads ...
- hvis det er succes rammer vi elementet

```java
public Value get(Key key)
{
  Node x = root;
  while (x != null)
  {
    int cmp = key.compareTo(x.key);
    if (cmp < 0)        x = x.left;
    else if (cmp > 0)   x = x.right;
    else if (cmp == 0)  return x.val;
  }
  return null;
}
```

### ANTAL COMPARES : dybde på træ + 1

--------------------------------------------------------------------------------
## unsuccesfuld/succesfuld insert

```java
public void put(Key key, Value val)
{  
  root = put(root, key, val);          // her ses at root allerede sættes til
                                      // hvis der ikke eksisterer en root
}

private Node put(Node x, Key key, Value val)
{
  if (x == null) return new Node(key, val);
  int cmp= key.compareTo(x.key);
  if (cmp < 0)
    x.left = put(x.left, key, val);   // her ses at man linker mens man putter
                                      // key/value - så hvis vi rammer New node
                                      // i næste kald
                                      // vil x.left blive linket til denne
  else if (cmp > 0)
    x.right = put(x.right, key, val); // samme som ovenfor...
                                      // bare med x.right
  else if (cmp == 0)
    x.val = val;                      //hvis noden allerede eksisterer
                                      //ændrer vi val...
  return x;
}
```
--------------------------------------------------------------------------------

# Træet opbygning - kommer an på hvordan nøgler indsættes!

- Best case : fuldstændig balanceret
- Worst case : kommer ind i "rækkefølge" - BST bliver en lang række!

--------------------------------------------------------------------------------

# Svarer til quick-sort partitioning ...
 Hvis vi indsætter N forskellige keys i random order -
 Så vil det forventede antal compares for search/insert være ~2lnN

 - Svarer til quick-sort partitioning

 Det viser sig ligeledes at den den dybden i dette tilfælde (random insert) også er højest 4.3N
