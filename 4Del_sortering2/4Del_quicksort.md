# QUICK SORT
1. blander array...  
2. partitioning ....
3. pivot element - mindre til venstre,- størrer til højre
4. Herefter rekursivt
--------------------------------------------------------------------------------
- Tony Hore opfinder 1961
- Bob Sedgwick optimerer ... herfter poupulær
--------------------------------------------------------------------------------
Scanner ned igennem array fra begge sider array indtil
venstre-pointer finder et der er for stort og
højre-pointer finder et der er for lille
de bytter rundt når det lykkes begge
og/eller stopper når de når krydser

--------------------------------------------------------------------------------
```java
public static void sort(Comparable[] a) {
StdRandom.shuffle(a);
sort(a, 0, a.length - 1);
}

private static void sort(Comparable[] a, int lo, int hi) {
if (hi <= lo) return;
int j = partition(a, lo, hi);
sort(a, lo, j-1);
sort(a, j+1, hi);
}

private static int partition(Comparable[] a, int lo, int hi) {
int i = lo, j = hi+1;
while (true) {
while (less(a[++i], a[lo]))
if (i == hi) break;
while (less(a[lo], a[--j]))
if (j == lo) break;
if (i >= j) break;
exch(a, i, j);
}
exch(a, lo, j);
return j;
}  
```

-------------------------------------------------------------------------------
# Egenskaber

- partition er in-place
- tricky at tjekke om pointers krydser ??
- counter-intutive - det er bedre at swappe elementer der =
- algoritmen kan køre langsomt hvis der ikke er tilfældighed ....
-------------------------------------------------------------------------------
# TIDSANALYSE

## BEST CASE : MIDTERSTE HVER GANG
sammenligner N
sammenligner N/2 + N/2
sammenligner N/4 + N/4 + N/4 + N/4
osv.
sammenligner 1   +   1 + ... +   1

Da vi deler med 2 hver gang bliver antallet af "kald" lgN, men hver gang laves N sammenligninger =~ N*lgN

## WORT CASE : VENSTRE SIDE HVER GANG
sammenligner N
sammenligner (N-1)
sammenligner (N-2)
osv.
sammenligner 1

Der tælles kun ned med en hver fang så sammlede antal sammenligninger er:
N + (N-1) + ... + 1 + 0 =~ 1/2*N^2

## GENNEMSNIT
~1.39NlgN

## LAS VEGAS algoritme : garanteret korrekt, afhænger af tilfældig shuffle

## Avereage : 39% flere compares end mergesort - hurtigere i praksis pga mindre daata flytning

## IKKE STABIL
-------------------------------------------------------------------------------

# FORBEDRING
bedre : pivot item = median

praktisk vælger median af tre ???
