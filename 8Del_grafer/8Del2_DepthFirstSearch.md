# Dybde først søgning

Eksempel : gennemsøgning af labyrint   
- Ruller en rulle garn
- markerer ukendte steder
- vender om når man når et kendt sted

Hvis algoritmen bliver ved ...
bliver alle steder vi kan nå - markeret !!!

-------
## implementation DFS

DFS(to visit v)   
Mark v as vsited    
Recursivly visit all umarked ajacent to v.
--------

- marked[] : Marker hvor vi har været
- edgeTo[] : Hvor vi kom fra edgeTo[3] = 5 betyder vi kom fra 5 til 3....

-------

edgeTo indeholder nu en mulighed for at sige hvilke knuder vi kan nå ... og hvordan ;-)

-------
## TID
> DFS markerer alle knuder forbundet til s i tid propertionelt til summen af deres grad... (plus initaliserings tid)
>>Bevis:
>>Alle knuder besøges en gang..

>Efter DFS kan man undersøge i konstant tid om s og v er forbundet
>og kan finde sti i tid propertionel til længden
>>Bevis:
>>edgeTo is parrent link representation to s....
