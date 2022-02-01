# 4L9IF0P3 - Analyse des données et datavisualisation 

## ***Les toilettes publiques sur le réseau RATP en Ile-de-France***

 
Mon étude porte sur les toilettes publiques sur les lignes RATP (régie autonome des transports parisiens) en Ile-de-France. Bien que les transports ferroviaires soient les plus plébiscités par les Franciliens et par les touristes étrangers et provinciaux pour se rendre à la capitale, je remarque que la plupart des toilettes publiques sont situées dans les grandes gares parisiennes telles que Paris Montparnasse, Paris Saint-Lazare, Paris Est, Paris Nord, Paris Austerlitz, Paris Gare de Lyon, Paris Bercy. De plus, la plupart d’entre elles sont payantes. *Petite anecdote : pour accéder aux toilettes situées à la gare Paris Saint-Lazare, il faut payer environ 1 € !* 
Puis, concernant les stations parisiennes et franciliennes desservies par le réseau RATP, j’ai rarement vu des toilettes publiques. 
C’est la raison pour laquelle, j’ai choisi de mener cette étude afin de mettre en évidence leur implantation ainsi que les conditions d’utilisation des toilettes publiques dans les stations parisiennes. 

Voici le tableau des données, issu du jeu de données OpenDatasoft : 

<iframe src="https://data.opendatasoft.com/explore/embed/dataset/sanitaires-reseau-ratp@dataratp/table/?&static=false&datasetcard=true" width="600" height="450" frameborder="0"></iframe>

*Ce tableau de données a été utilisé pour réaliser un graphique, uniquement dans la partie 1, b.* 

---------------------------------------------------------

> Sommaire 

[Partie 1 : Le nombre de toilettes publiques sur les lignes RATP](partie1A.md) 
   * [a. Généralités](partie1A.md)
   * [b. Les stations équipées des toilettes publiques](partie1B.md) 

[Partie 2 : Les toilettes publiques gratuites et payantes](partie2.md)

[Partie 3 : L’accès aux toilettes publiques sur le réseau RATP](partie3A.md)
   * [a. Pour les personnes à mobilité réduite (PMR)](partie3A.md)
   * [b. En zone contrôlée et en hors zone contrôlée](partie3B.md)

___________________________________________________________



Partie 1 : Le nombre de toilettes publiques sur les lignes RATP

   * a. Généralités 

Cette carte représente le nombre de stations RATP qui possèdent des toilettes publiques en Ile-de-France. Grâce aux coordonnées géographiques, la plupart d’entre elles sont situées dans Paris, grâce aux métros parisiens. Les autres sont situées dans la région parisienne par le biais des autres lignes RATP. 

<div class="flourish-embed flourish-map" data-src="visualisation/8573833"><script src="https://public.flourish.studio/resources/embed.js"></script></div>

Pour connaître la localisation des toilettes publiques RATP en Ile-de-France, j’ai voulu utiliser Flourish, à partir du fichier Excel téléchargé sur le site Open Data RATP. En revanche, je me suis heurtée à quelques difficultés. En effet, les résultats attendus ne s'affichent pas sur Flourish. Par conséquent, j’ai utilisé OpenRefine pour la raison suivante :
- Avant le nettoyage des données : dans la colonne consacrée aux coordonnées géographiques, la latitude ainsi que la longitude sont rassemblées sur une seule colonne, dont séparées uniquement par une virgule. En utilisant l’outil Opendatasoft, je n’ai pas rencontré de soucis. En revanche, lorsque j’ai voulu utilisé Flourish pour éditer une carte, toutes les informations importées à partir des fichiers Excel ou du fichier CSV n’ont pas été prises en compte. Par conséquent, il a fallu procéder au *"datawrangling"* (ou nettoyage des données). 

Sur OpenRefine, j’ai procédé à quelques modifications. J’ai dû : 
- Réconcilier les noms de stations franciliennes desservies par le réseau RATP, qui possèdent des toilettes publiques (en les considérant comme des stations ferroviaires).  A la fin, toutes ont une propriété Wikidata attribuée, comme l'exemple dans la capture d'écran :

![Capture d’écran 2022-02-01 à 17 39 26](https://user-images.githubusercontent.com/97068887/152011001-b4e5eb0e-d978-4083-ba26-38b5c7eb112d.png)
*Capture d'écran de la page provenant d'OpenRefine*

- Renommer les noms des colonnes, en évitant des espaces. 
- Diviser en plusieurs colonnes la colonne coord_geo transformée en deux dont : 
  - Une colonne qui rassemble les latitudes
  - Une autre colonne qui rassemble les longitudes
- Remplir les cases vides 

Voici l'historique des modifications : 
```json
[
  {
    "op": "core/recon",
    "engineConfig": {
      "facets": [],
      "mode": "row-based"
    },
    "columnName": "Station",
    "config": {
      "mode": "standard-service",
      "service": "https://wikidata.reconci.link/en/api",
      "identifierSpace": "http://www.wikidata.org/entity/",
      "schemaSpace": "http://www.wikidata.org/prop/direct/",
      "type": {
        "id": "Q55488",
        "name": "railway station"
      },
      "autoMatch": true,
      "columnDetails": [],
      "limit": 0
    },
    "description": "Reconcile cells in column Station to type Q55488"
  },
  {
    "op": "core/recon-judge-similar-cells",
    "engineConfig": {
      "facets": [],
      "mode": "row-based"
    },
    "columnName": "Station",
    "similarValue": "Antony",
    "judgment": "matched",
    "match": {
      "id": "Q2341704",
      "name": "Gare d'Antony",
      "types": [
        ""
      ],
      "score": 100
    },
    "shareNewTopics": false,
    "description": "Match item Gare d'Antony (Q2341704) for cells containing \"Antony\" in column Station"
  },
  {
    "op": "core/column-split",
    "engineConfig": {
      "facets": [],
      "mode": "row-based"
    },
    "columnName": "coord_geo",
    "guessCellType": true,
    "removeOriginalColumn": true,
    "mode": "separator",
    "separator": ",",
    "regex": false,
    "maxColumns": 0,
    "description": "Split column coord_geo by separator"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "coord_geo 1",
    "newColumnName": "coord_geo_latitude",
    "description": "Rename column coord_geo 1 to coord_geo_latitude"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "coord_geo 2",
    "newColumnName": "coord_geo_longitude",
    "description": "Rename column coord_geo 2 to coord_geo_longitude"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "Accessible au public",
    "newColumnName": "Accessible_au_public",
    "description": "Rename column Accessible au public to Accessible_au_public"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "Tarif [Gratuit|Payant]",
    "newColumnName": "Tarif_Gratuit_Payant",
    "description": "Rename column Tarif [Gratuit|Payant] to Tarif_Gratuit_Payant"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "Acces Passe Navigo ou Ticket T+",
    "newColumnName": "Acces_Passe_Navigo_ou_Ticket_T_plus",
    "description": "Rename column Acces Passe Navigo ou Ticket T+ to Acces_Passe_Navigo_ou_Ticket_T_plus"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "Acces Bouton poussoir",
    "newColumnName": "Acces_Bouton_poussoir",
    "description": "Rename column Acces Bouton poussoir to Acces_Bouton_poussoir"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "En zone controlee",
    "newColumnName": "En_zone_controlee",
    "description": "Rename column En zone controlee to En_zone_controlee"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "Hors zone controlee station",
    "newColumnName": "Hors_zone_controlee_station",
    "description": "Rename column Hors zone controlee station to Hors_zone_controlee_station"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "Hors zone controlee voie publique",
    "newColumnName": "Hors_zone_controlee_voie_publique",
    "description": "Rename column Hors zone controlee voie publique to Hors_zone_controlee_voie_publique"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "Accessibilite PMR",
    "newColumnName": "Accessibilite_PMR",
    "description": "Rename column Accessibilite PMR to Accessibilite_PMR"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "coord_geo_latitude",
    "newColumnName": "latitude",
    "description": "Rename column coord_geo_latitude to latitude"
  },
  {
    "op": "core/column-rename",
    "oldColumnName": "coord_geo_longitude",
    "newColumnName": "longitude",
    "description": "Rename column coord_geo_longitude to longitude"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [],
      "mode": "row-based"
    },
    "columnName": "En_zone_controlee",
    "expression": "value",
    "edits": [
      {
        "from": [
          ""
        ],
        "fromBlank": true,
        "fromError": false,
        "to": "non"
      }
    ],
    "description": "Mass edit cells in column En_zone_controlee"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [],
      "mode": "row-based"
    },
    "columnName": "Acces_Passe_Navigo_ou_Ticket_T_plus",
    "expression": "value",
    "edits": [
      {
        "from": [
          ""
        ],
        "fromBlank": true,
        "fromError": false,
        "to": "non"
      }
    ],
    "description": "Mass edit cells in column Acces_Passe_Navigo_ou_Ticket_T_plus"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [],
      "mode": "row-based"
    },
    "columnName": "Hors_zone_controlee_station",
    "expression": "value",
    "edits": [
      {
        "from": [
          "non"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "non"
      }
    ],
    "description": "Mass edit cells in column Hors_zone_controlee_station"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [],
      "mode": "row-based"
    },
    "columnName": "Hors_zone_controlee_station",
    "expression": "value",
    "edits": [
      {
        "from": [
          ""
        ],
        "fromBlank": true,
        "fromError": false,
        "to": "non"
      }
    ],
    "description": "Mass edit cells in column Hors_zone_controlee_station"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [],
      "mode": "row-based"
    },
    "columnName": "Acces_Bouton_poussoir",
    "expression": "value",
    "edits": [
      {
        "from": [
          ""
        ],
        "fromBlank": true,
        "fromError": false,
        "to": "non"
      }
    ],
    "description": "Mass edit cells in column Acces_Bouton_poussoir"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [],
      "mode": "row-based"
    },
    "columnName": "Hors_zone_controlee_voie_publique",
    "expression": "value",
    "edits": [
      {
        "from": [
          "non"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "non"
      }
    ],
    "description": "Mass edit cells in column Hors_zone_controlee_voie_publique"
  },
  {
    "op": "core/mass-edit",
    "engineConfig": {
      "facets": [],
      "mode": "row-based"
    },
    "columnName": "Hors_zone_controlee_voie_publique",
    "expression": "value",
    "edits": [
      {
        "from": [
          ""
        ],
        "fromBlank": true,
        "fromError": false,
        "to": "non"
      }
    ],
    "description": "Mass edit cells in column Hors_zone_controlee_voie_publique"
  }
]
```

Après cette modification, j’ai téléchargé le fichier en format Excel. Cette carte éditée avec Flourish provient du fichier nettoyé à l’aide d’OpenRefine, téléchargé au même format et importé. J'ai notamment utilisé ce même fichier pour créer des graphiques sur Rawgraphs. 

Voici le tableau de données retravaillé à partir d'OpenRefine, et importé dans Datawrapper :
<iframe title="Toilettes publiques dans le réseau RATP " aria-label="Tableau" id="datawrapper-chart-3S7Q5" src="https://datawrapper.dwcdn.net/3S7Q5/4/" scrolling="no" frameborder="0" style="width: 0; min-width: 100% !important; border: none;" height="2073"></iframe><script type="text/javascript">!function(){"use strict";window.addEventListener("message",(function(e){if(void 0!==e.data["datawrapper-height"]){var t=document.querySelectorAll("iframe");for(var a in e.data["datawrapper-height"])for(var r=0;r<t.length;r++){if(t[r].contentWindow===e.source)t[r].style.height=e.data["datawrapper-height"][a]+"px"}}}))}();
</script>


   * b. Les stations équipées des toilettes publiques

Ce graphique représente le nombre de toilettes publiques par ligne RATP. 
Le RER A possède 21 toilettes publiques. En effet, le RER A fait partie des lignes principales en Ile-de-France. Selon les médias, elle est empruntée par des millions de voyageurs, que ce soit par les touristes ou par les travailleurs. Ensuite, le RER B possède 11 toilettes publiques.
Du côté du métro parisien, six lignes possèdent chacune une toilette publique, comme les lignes 1, 5, 6, 7, 10 et 12. 
Nous avons repéré certaines stations qui possèdent autant de toilettes publiques. Voici les exemples :
- Les stations Charles de Gaulle-Etoile (lignes 1 et RER A) et Châtelet-les-Halles (RER A) possèdent trois toilettes publiques. Cela est dû aux multiples correspondances avec les lignes de métro. Pour les personnes pressées ou pour celles qui n’ont pas de jetons, ces toilettes leur sont bénéfiques. Cela leur évite de rentrer dans les toilettes des centres commerciaux (notamment au Forum des Halles) puisqu’elles sont payantes. 
- La station Noisy Le Grand-Mont d’Est possède deux toilettes publiques. 
- La station Gare de Lyon possède deux toilettes publiques. 
- La station Saint-Germain-en-Laye possède deux toilettes publiques. Celles-ci sont proches d’un site touristique, comme le château et le parc par exemple.  


<iframe src="https://data.opendatasoft.com/chart/embed/toilettespubliques_ratp_graphique/?&static=false&datasetcard=false" width="600" height="450" frameborder="0"></iframe>
Source : OpenDatasoft 
(https://data.opendatasoft.com/chart/embed/toilettespubliques_ratp_graphique/)



Partie 2 : Les toilettes publiques gratuites et payantes

Nous avons repéré des toilettes publiques gratuites et des toilettes publiques payantes, à l’aide de l’outil Rawgraphs. 

![lineardendrogram](https://user-images.githubusercontent.com/97068887/151880748-063daf1e-abae-497b-be5e-e306218710c1.svg)

Source : Rawgraphs  (NB : ceci a été réalisé à partir du tableau de données retravaillé avec OpenRefine) 
 
Parmi les 48 stations, 2 d’entre elles possèdent des toilettes publiques payantes. Il s’agit de : 
- la station Cluny la Sorbonne, desservie par la ligne 10
- l'une des deux toilettes publiques situées à la station Saint-Germain-en-Laye, desservie par le RER A (d’où la couleur verte inscrite dans la légende signifiant que parmi les deux toilettes publiques situées aux différents endroits, l'une d'entre elles a un accès payant)
Ces deux stations sont situées vers des sites touristiques, voire dans des quartiers les plus aisés. 

Les autres stations possèdent des toilettes publiques gratuites. En première position, on retrouve la station Châtelet-les-Halles qui détient trois toilettes publiques gratuites, suivie des stations comme Charles de Gaulle-Etoile et Noisy-le-Grand Mont d’Est possédant deux toilettes publiques gratuites. 


Partie 3 : L’accès aux toilettes publiques sur le réseau RATP
 
   * a. Pour les personnes à mobilité réduite (PMR)
 
Avec Rawgraphs, nous avons voir le nombre de toilettes publiques équipées d’un accès pour les personnes à mobilité réduite sur le réseau RATP. 

![treemap2](https://user-images.githubusercontent.com/97068887/152008025-21ef06d1-564f-4cfe-81f0-774c41ef4ef8.svg)

Source : Rawgraphs  (NB : ceci a été réalisé à partir du tableau de données retravaillé avec OpenRefine) 

La plupart des stations possèdent des toilettes accessibles aux PMR, sauf pour les 5 stations telles que : 
- Bobigny - Pablo Picasso
- Charles de Gaulle - Etoile (sortie avenue Carnot, après la ligne de valideurs en venant de l’extérieur de la gare)
- Charles de Gaulle - Etoile (en entrant par l’accès 3, avenue Hoche, dans le couloir menant vers la sortie 2, avenue de Friedland)
- Cité Universitaire 
- Denfert Rochereau

   * b. En zone contrôlée et en hors zone contrôlée voie publique 

Les toilettes situées en zone contrôlée sont accessibles après avoir validé le titre de transport. Les toilettes peuvent se situer sur les quais par exemple (à l’avant ou à l’arrière du quai). 
Les toilettes situées hors zone contrôlée sont positionnées à l’entrée des gares ou à côté de la gare, située à l’extérieur. Pour montrer cela, j'ai utilisé Rawgraphs pour mettre l'accent sur les toilettes publiques situées sur les voies publiques uniquement. 
 
![viz](https://user-images.githubusercontent.com/97068887/151870066-b7b1395d-ba4d-44dc-b613-fc1310dbfa43.svg)

Source : Rawgraphs  (NB : ceci a été réalisé à partir du tableau de données retravaillé avec OpenRefine) 

Certaines toilettes publiques hors zone contrôlée, notamment en voie publique, demandent aux passagers d’avoir des tickets t+ ou Pass Navigo pour y accéder, notamment dans les stations telles que : 
- Arcueil Cachan
- Cluny - La Sorbonne
- La Place
- Massy-Palaiseau
- Saint-Maur - Créteil
- Saint-Rémy-les-Chevreuse
- Villejuif - Louis Aragon 


:---: |C'est par ceci que mon étude sur ce sujet bien particulier se termine. Merci pour votre attention !|
 
