# Deletion

Mark it with a "tombstone"....    
Og lade som om den ikke er der ...    
Men det er selvfølgelig ikke så smart i længden     

--------------------------------------------------------------------------------

### Fjern minimum ...

- gå til venstre indtil man finder en node med left=null
- replace noden med den højre
- opdater counts

```java
public void deleteMin()
{ root = deleteMin(root); }
private Node deleteMin(Node x)
{
if (x.left == null) return x.right;
x.left = deleteMin(x.left);
x.count = 1 + size(x.left) + size(x.right);
return x;

}
```

Virker også for delete maksimum...

--------------------------------------------------------------------------------
### Generel Deletion
### Kaldes Hibbard deletion

Cases
- ingen børn : ingen problemer
- et barn : ingen problemer
- to børn: ....

to børn:
- find det næste - mindste node - i subtræet
- find minimum M delete minimum ...
- erstat minimum M med node der skal fjernes

```java
public void delete(Key key)
{ root = delete(root, key); }
private Node delete(Node x, Key key) {
if (x == null) return null;
int cmp = key.compareTo(x.key);
if (cmp < 0) x.left = delete(x.left, key);
else if (cmp > 0) x.right = delete(x.right, key);
else {
if (x.right == null) return x.left;
if (x.left == null) return x.right;
Node t = x;
x = min(t.right);
x.right = deleteMin(t.right);
x.left = t.left;
}
x.count = size(x.left) + size(x.right) + 1;
return x;
}
```

--------------------------------------------------------------------------------
### Hibbert deletion leder til asymetri ...

Overraskende nok bliver træ højde sqrt(N) og ikke lg(N) efter mange delete og insert

Longstanding open problem : Simple og effektiv delete for BST's
Der sidste 50 år har ingen endnu opdaget nogen ......
