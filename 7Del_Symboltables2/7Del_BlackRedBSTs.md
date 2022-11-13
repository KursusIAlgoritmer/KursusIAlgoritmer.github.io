# Balanced search trees : red-black BST

Man repræsenterer 2-3tree som et BST...

Det betyder vi skal have en repræsentation for 3node:
- største key : root
- "rødt" link forbinder dem
- midste key er venstre child - dennes højre child er mellem de største og mindste


--------------------------------------------------------------
Search er det samme som BST!!
osv.
--------------------------------------------------------------

- Alle red-links læner til venstre ...

--------------------------------------------------------------
### Implementation

Node udvides med boolean color RED(true) eller BLACK(false)
der illustrerer link til forældrer!!

- bliver nødt til at have såkaldt "left-rotation"
```java
private Node rotateLeft(Node h){
  assert isRed(h.right);
  Node x = h.right;    
  h.right = x.left;
  x.left = h;
  x.color = h.color;
  h.color = RED;
  return x;
}
```

- rotateRight
Byt bare rundt på left og right


- bliver også nødt til at have en "color-flip"
flip alle farver!!!!

--------------------------------------------------------------
### Eksempel

indsæt C på A
- sættes først til højre for A - med et rødt link
(hver gang vi tilføjer en nøde laver vi rødt-link)
- derefter "left rotate"

indsæt i et træ med en node
- hvis den er til venstre så er vi færdige
- til højre så må vi rotere til venstre

Der er kun to nodes - dvs en single 3-node
Case 1 : indsætter størrer node
- Der kommer to røde links - derfor flip colors
Case 2 : indsætter MINDRE
- der kommer to røde links i rækkefølge
- roterer til højre
- flipper color
Case 3 : midt imellem
- roter først nederste rotateLeft
- roter til højre
- flip colors

--------------------------------------------------------------
```java
private Node put(Node h, Key key, Value val){
  if (h == null) return new Node(key, val, RED);
  int cmp = key.compareTo(h.key);
  if (cmp < 0)        h.left = put(h.left, key, val);
  else if (cmp > 0)   h.right = put(h.right, key, val);
  else if (cmp == 0)  h.val = val;
  if (isRed(h.right) && !isRed(h.left))     h = rotateLeft(h);
  if (isRed(h.left) && isRed(h.left.left))  h = rotateRight(h);
  if (isRed(h.left) && isRed(h.right))      flipColors(h);
  return h;
}
```
