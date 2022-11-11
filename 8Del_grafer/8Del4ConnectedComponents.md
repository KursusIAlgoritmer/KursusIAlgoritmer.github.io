# Connected Components - Forbundne komponenter

Spørgsmålet er v og w forbundne?   

Det kunne vi svare på med UninFind ... men dette var en mere kompliceret situation hvor der blev ændret i strukturen undervejs...
Det bliver der ikkke i grafen - derfor er denne hurtigere...

???Hvorfor kan man egentlig ikke bare ændre grafen ??

> Equvivalence relation :
>> Reflexive
>> Symmetric
>> Transitive

---------------------------------------------------

Kør DFS fra alle umarkerede knuder for at identificere alle knuder der har samme komponent

Ny anvendt "datastruktur":    
id[] : der indeholder komponentens nummer
 
---------------------------------------------------
