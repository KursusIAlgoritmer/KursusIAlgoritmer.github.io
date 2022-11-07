# KursusIAlgoritmer.github.io

# Chapter 1.5 - Union-find

En bestemt "datastruktur" der hedder "foren-og-find" på dansk.
https://www.geeksforgeeks.org/difference-between-abstract-and-concrete-data-structure/.


Foren-og-find løser problemet kaldet "dynamisk sammenhæng"!
Dynmaisk sammenhængs problemet er defineret ved tre ting:
- der eksisterer et antal elementer N
- der findes en "foren" operation , union(a,b)
- der findes en "er forbunde?" også kaldet "find" operation, connected(a,b)

Probelemet er hvordan implementeres en datastruktur der kan løse problemet

Dens formål
----
https://www.youtube.com/embed/xmbjs-rQf4k
----

## Findes ikke i noget standardbibliotek

- void connect(A,B)     : dette er en dynamisk operation
- boolean isConnected(A,B) : ækvivalensrelation - dvs. isConnected er "refelksiv","symetrisk" og "transitiv"

## Sammenhængskomponenter : Algoritme terminologi ( i matematik kalder man det ...)

- Hvis 1,2 og 3 hænger sammen
- Når man forener elementer fra to forskellige sammenhængskomponenter - forenes sammenhængskomponenterne

## Lav en "foren og find" datastruktur !!

```java

public interface UF{

  public UF(int n);

  public void union(int a, int b);

  public int find(int a);

  public boolean isConnected(int a, int b)

}

```

En default implementation af "isConnected":

```java

  public boolean isConnected(int a, int b){
    return find(a) == find(b);
  }

```
------------------------------------------------------------------------------------------------------------
# Hurtig-find implementation af union-find ...

- Array af heltal id[] med længde N
- fortolkning id[p] er ID'et for komponenten (sammenhængskomponenten) der  


Her er en collection af mit kode arbejde til algoritmer kuset....

[https://editor.p5js.org/ajrp/collections/nn03rywN0](https://editor.p5js.org/ajrp/collections/nn03rywN0)

Her er mit min "p5js kode" til quick-find :

```javascript


function find(a) {
  return ids[a];
}


function union(a, b) {
  //første ide : Erstate alle indgange der er lig "ids[a]" med "ids[b]"

  //indsætter elementer hvis de ikke eksisterer --- nødvendigt fordi jeg starter med ukendt længde modsat bog
  ids[a] = ids[a] == undefined ? a : ids[a];
  ids[b] = ids[b] == undefined ? b : ids[b];

  //Dette retter fejlen fra version2 - vi husker ID'er inden gennemløb
  let idA = ids[a];
  let idB = ids[b];

  for (let i = 0; i < ids.length; i++) {
    if (ids[i] == idB) {
      ids[i] = idA; //alle andre idB ID'er sættes til idA
    }
  }
}

function isConnected(a, b) {
  return find(a) === find(b);
}

```
------------------------------------------------------------------------------------------------------------
## Kørselstid quick-find

| opret | foren | find | forbundne |
| ------| ----- | ---- | --------- |
| N     | N     | 1    | 1         |

Det vi tæller er antal gange vi tilgår hukommelsen - i vores tilfælde er dette hvornår vi læser eller skriver til vores array

## Foren N tager N^2 tid

------------------------------------------------------------------------------------------------------------
# Hurtig-forening - quick union



## VIDEO TID 46:50

***CITAT TID 46: 50***
***EN DATASTRUKTUR ER TILSTANDEN OG DE UNDERLIGGENDE ALGORITMER DER ER NØDVENDIGE FOR AT ÆNDRE DEN TILSTAND***

**Citat fortsættes...***
***Lidt ligesom et objekt, med data og dertilhørende metoder***


## VIDEO TID 49:15

***MEGET VIGTIG REMINDER .... NÅR TO ELEMENTER p OG q SKAL FORENES ER DET NØDVENDIGT AT FÅ DEN ENES ROD TIL AT PEGE PÅ DEN ANDENS ROD!!!!***    
***HVIS BARE MAN SKIFTER ps TIL AT PEGE PÅ DEN ANDEN KAN DEN MIDSTE DET FORBINDELSE DEN HAR TIL DENS OPRINDELIGE KOMPONENT***


mit forslag til kode der implementerer quick-union :

```javascript
function findRoot(a){

  if(ids[a] == undefined) return;  //hvis ikke a eksisterer stop!

  while(a!=ids[a]){
    a = ids[a];    
  }

  return a;
}

function union(a, b) {  
  //indsætter elementer hvis de ikke eksisterer --- nødvendigt fordi jeg starter med ukendt længde modsat bog
  ids[a] = ids[a] == undefined ? a : ids[a];
  ids[b] = ids[b] == undefined ? b : ids[b];

  rootA  = findRoot(a);
  rootB  = findRoot(b);

  //Er det her rigtigt??????
  //man kunne nøjes med at sætte den ene til et pege på den anden ... men træet vil vokse -
  //og der vil da være størrer omkostninger forbundet ved at finde roden senere

  ids[rootA] = rootB;

}


function isConnected(a, b) {
  return findRoot(a) === findRoot(b);
}
```

------------------------------------------------------------------------------------------------------------
## Kørselstid quick-union

| opret | foren | find | forbundne |
| ------| ----- | ---- | --------- |
| N     | N     | N    | N         |

------------------------------------------------------------------------------------------------------------

## Hurtig find er defekt
- forening er for dyr ( n arrayadgange)
- træer er flade - men det er dyrt

## Hurtig forening er defekt
- træerne kan i værste fald blive lige så høje som antallet af elementer
- find (og dermed også foren) er for dyr (op til n arrayadgange)

------------------------------------------------------------------------------------------------------------
# Forbedring : weighted quick-union

få det lille træ til at pege på det store træs rod...     
Når man senere skal søge i træet vil det ikke tage lige så længe

***VIGTIGT : her menes der ikke højde men antal elementer***


## VIDEO TID 1:18:34
```diff

- SÆTNING : DYBDEN AF ENHVER KNUDE X ER HØJEST lg(N)
lg: er 2-tals logaritmen

+ BEVIS:
+ 1.) Når en knudes dybde stiger er det fordi den bliver forenet med et andet træ
+ 2.) Når en knudes dybde stiger er det med 1 fordi roden af det ene træ T1 sættes fast på roden af det andet T2
+ 3.) Hver gang to træer forenes bliver størrelsen mindst dobbelt så stor som det mindste træ
+ 4.) Antal foreninger, der skal til for at forene alle knuder må være mindre end lg(N)
+ 5.) Antallet af foreninger svarer til den maksimale dybde for en knude
+ 6.) Den maksimale dybde for en knude er højest lg(N)
```
|operation| tid|
| ------| --------- |
| find. | tager tid propertionelt med dybden af p |
| foren | tager kostant tid, hvis vi har rødderne! ( har vi rødderne?) |

------------------------------------------------------------------------------------------------------------
## Kørselstid weighted-quick-union

| opret | foren | find | forbundne |
| ------| ----- | ---- | --------- |
| N     | lg(N) | lg(N)| lg(N)     |

* *alle omkostninger handler om at finde rødder - da de har dybden højest lg(N) - tager det altså lg(N)*

------------------------------------------------------------------------------------------------------------
# Forbedring : path compression

Efter vi har rørt en knude ... så sæt den til at pege på roden...

## Varianter :

## 1.) To-pas implentation:

en løkke mere

## 2.) Enklere ét-pas variant (vejhalvering):

```java
public int find(int i){
  while(i != id[i]){
    id[i]= id[id[i]];   //kun en ekstra linje !!!!!!
    i = id[i];
  }
  return i;
}
```

## Meget elegant vejforkortning fra video tid : 1:30:50

```java

public int find(int a){
  if(a==p[a]) return a;
 return p[a] = find(p[a]);
}

```

```diff

-  Vægtet hurtig-forening med vejforkortning : amortiseret analyse
lg. : er 2-tals logaritmen
lg* : er antal gange vi skal tage lg for at nå til 1

- SÆTNING:
- Enhver sekvens af M operationer på N elementer  koster <= c(N+M lg*(N)) arrayadgange
- analyse : kan forbedres til N + M alpha (m,N)
- simpel algoritme med fascinerende matematik
```

# AMORTISERET tid 1:34:16

Citat :  

Robust måde at sig den gennemsnitlige udførselstid ... kan være uheldig hvis man siger "den gennemsnitlige udførselstid" at den vil være fuldstændigt åndsvag stor ... her siger man "det kan ikke ske" ... man kan kun få en dyr operation hvis man har en masse billige operationer, der sparer op til den dyre operation.

Gennemsnit kan skjule en masse grimme ting. Amortiseret kan ikke skjule grimme ting. Vi er garanteret...

------------------------------------------------------------------------------------------------------------

Ingen lineær foren_og_find men tæt på...'

# OPSUMMERING

M er antal operationer  
N er antal elementer.

| algoritme | værste tid |
| ------ | --------- |
| hutig -find     | M*N |
| hutig -find     | M*N |
| vægtet hurtig forening | N + M*lg(N) |
| hutig forening + vejforkortning | N + M*lg(N) |
| alt! | N + M*lg*(N) |

TROR DER ER EN FEJL I VIDOEN DER STÅR log OG IKKE lg tid 1:37:44
------------------------------------------------------------------------------------------------------------

# ANVENDELSE

- Spillet Go
- Kruskals algoritme til mindst udspændte træ
- DK statestik def. byområde
- Perkolation (kan man gennemtrænge - kan væsken sive ned igennem) socialt-netværk, elektricitet eller...
- der er flere
