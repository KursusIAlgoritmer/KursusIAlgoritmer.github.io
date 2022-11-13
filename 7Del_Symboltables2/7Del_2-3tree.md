# Balanced search trees

Vi vil gerne garantere at vi anvender lgN

2-3 search trees

--------------------------------------------------------------------------------
opbygning_
- 2-node : 1 key , 2 childeren
- 3-node : 2 key , 3 childeren

3 node:
- left : MINDRE
- middle : imellem de to keys
- right : størrer

Egenskaber:   
- Pefekt balance: alle veje fra root til null-link har samme længde!!!
- Symetrisk orden: inorder traversal giver nøgler i ligefrem rækkefølge



--------------------------------------------------------------------------------
Søgning:

--------------------------------------------------------------------------------
Indsætning:
- Hvis man indsætter i en 2-node - bliver det bare til en 3-node
- Hvis man indsætter i en 3-node - transformerer den 2x2nodes om og forældren bliver 3node

?!?"?"&"%"


--------------------------------------------------------------------------------
Hvorfor er der balance i et 2-3 tree ??...   
Vi ser på alle transformationer:

root:
- split root -> laver en balanceret træet

parent in 2-node:
- split lift/right child -> flytter bare child en op

parent in 3-node:
- left ...
- middle ...
- right

--------------------------------------------------------------------------------

Hvor lang kan træet blive

- Hvis alt er 2-nodes : er dette det højest muliged - og det er lgN
- Hvis alt er 3 nodes : 0.631 * lgN


12 til 20 for en million nodes, 18 til 30 for en milliard

Alle operationer er c*lgN !!!!!!!!!!!!!
