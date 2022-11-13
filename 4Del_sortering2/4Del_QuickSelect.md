# Quick Select
-------------------------------------------------------------------------------
## Find det k-th mindste element

## Brug teorien som guide ... n*logN øvre grænse ...
- sorter array
- kig på det k-th element

## Brug teorien som guide ... øvre grænse på N for k=1,2,3

## Brug teorien som guide ... nedre grænse N

-------------------------------------------------------------------------------
Virkemåde:
- pivot
- kører kun partition videre i venstre side når den er størrer end k'th
- ellers kører partitioning på højre

-------------------------------------------------------------------------------
## Den tager linær tid i gennemsnit!!

-------------------------------------------------------------------------------
Problem, hvis der er identiske nøgler...

- stop og flyt når der er identiske nøgler - kontra intuitivt
- DETTE ER FOR LAVE PARTITIONING I MIDTEN!!
-------------------------------------------------------------------------------
## Forbedring
## 3-ways partitioning
3 pointers  istedet for 2 ... ellers ligeledes som alm.
