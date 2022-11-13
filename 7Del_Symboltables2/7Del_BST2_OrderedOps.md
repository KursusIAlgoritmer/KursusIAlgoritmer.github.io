# Ordered operations

Find minimum og maximum

- Enten kan søg kun højre eller kun venstre
--------------------------------------------------------------------------------
Computing floor : find nærmeste er ligmed eller størrer end K

- LIG MED (k=k)   : fundet
- MINDRE  (k<node): gå til venstre
- STØRRER (k>node): så er floor den højre side og altså noden

```java
public Key floor(Key key)
{
  Node x = floor(root, key);
  if (x == null) return null;               //speciel case : der er ingen root
  return x.key;
}

private Node floor(Node x, Key key)
{
  if (x == null) return null;
  int cmp = key.compareTo(x.key);
  if (cmp == 0) return x;
  if (cmp < 0) return floor(x.left, key);   //hvis den er mindre fortsæt

  Node t = floor(x.right, key);             //tricky kode der ...
  if (t != null)  return t;
  else            return x;
}
```
--------------------------------------------------------------------------------
Ceeeling ... samme
--------------------------------------------------------------------------------
SUBTREE COUNTS

- i hver node gemmer vi antallet af nodes i sub-træet
- faciliterer "rank" og "select"

en implementation af size-opdatering er f.eks.:
```java
public int size(){
  return size(root);
}

private int size(Node x){
  if (x == null) return 0;
  return x.count;
}

private Node put(Node x, Key key, Value val){
  if (x == null)      return new Node(key, val, 1);
  int cmp = key.compareTo(x.key);
  if (cmp < 0) x.left = put(x.left, key, val);
  else if (cmp > 0)   x.right = put(x.right, key, val);
  else if (cmp == 0)  x.val = val;
  x.count = 1 + size(x.left) + size(x.right);
  return x;
}
```
--------------------------------------------------------------------------------
Rank : keys < k

Er vel bare SIZE af det venstre subtree????

- mangler lige at  

???????????????
--------------------------------------------------------------------------------
Inorder traversal...

-laver en kø

```java
public Iterable<Key> keys(){
  Queue<Key> q = new Queue<Key>();
  inorder(root, q);
  return q;
}

private void inorder(Node x, Queue<Key> q){
  if (x == null) return;
  inorder(x.left, q);
  q.enqueue(x.key);
  inorder(x.right, q);  
}
```
--------------------------------------------------------------------------------
# TIDER
Alle proportionelle til træets højde

hvis indsættelser er foregået tilfældigt giver ~2lnN

MEGET BEDRE END BINARY SEARCH I ET ORDNET ARRAY - der ikke er dynamisk og
desuden langsom til insertion(N)
