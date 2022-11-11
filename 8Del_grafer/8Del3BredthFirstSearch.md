# Del 7 - del 3 - Bredde først - Breadth First
- Gentag indtil kø er tom:
- Fjern v fra kø
- Tilføj alle umarkerede knuder der er forbundet  til v og marker dem

----------------------------------

Nødvendige "data-strukturer":
- queue : køen holder styr på hvor vi er nået til ....
- edgeTo[] : Hvorfra kom man til denne knude. edgeTo[1] = 0 betyder man kom fra 0 til 1
- distTo[] : distTo[] betyder afstanden. distTo[1] = 1 betyder afstenden er 1 til 1 fra s ( s er startknuden)

----------------------------------

> BFS : beregner de korteste veje fra s til alle andre knuder t id propertionelt til E + V

----------------------------------

Den grundlæggende forskel imellem BFS og DFS er at den ene bruger en "stak" og den anden en "kø"

----------------------------------
