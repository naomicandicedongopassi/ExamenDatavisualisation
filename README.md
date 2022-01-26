# 4L9IF0P3 - Analyse des données et datavisualisation 

## **Les toilettes publiques sur le réseau RATP en Ile-de-France**
 
Mon étude porte sur les toilettes publiques sur les lignes RATP (régie autonome des transports parisiens) en Ile-de-France. Bien que les transports ferroviaires soient les plus plébiscités par les Franciliens et par les touristes étrangers et provinciaux pour se rendre à la capitale, je remarque que la plupart des toilettes publiques sont situées dans les grandes gares parisiennes telles que Paris Montparnasse, Paris Saint-Lazare, Paris Est, Paris Nord, Paris Austerlitz, Paris Gare de Lyon, Paris Bercy. De plus, la plupart d’entre elles sont payantes. Puis, concernant les stations parisiennes et franciliennes desservies par le réseau RATP, j’ai rarement vu des toilettes publiques. 
C’est la raison pour laquelle, j’ai choisi de mener cette étude afin de mettre en évidence leur implantation ainsi que les conditions d’utilisation des toilettes publiques dans les stations parisiennes. 

Voici le tableau des données, issu du jeu de données OpenDatasoft 

<iframe src="https://data.opendatasoft.com/explore/embed/dataset/sanitaires-reseau-ratp@dataratp/table/?&static=false&datasetcard=false" width="600" height="450" frameborder="0"></iframe>



> Sommaire 

1. Le nombre de toilettes publiques sur les lignes RATP 
   * a. Généralités
   * b. Les stations équipées des toilettes publiques 

2. Les toilettes publiques gratuites et payantes

3. L’accès aux toilettes publiques sur le réseau RATP
   * a. Pour les personnes à mobilité réduite (PMR) 
   * b. En zone contrôlée et en hors zone contrôlée 

___________________________________________________________



1. Le nombre de toilettes publiques
   * a. Généralités 

Cette carte représente le nombre de stations RATP qui possèdent des toilettes publiques en Ile-de- France. Grâce aux coordonnées géographiques, la plupart d’entre elles sont situées dans Paris, grâce aux métros parisiens. Les autres sont situées dans la région parisienne par le biais des autres lignes RATP. 




Pour connaître la localisation des toilettes publiques RATP en Ile-de-France, j’ai voulu utiliser Datawrapper, à partir du fichier CSV téléchargé sur le site Data Ile-de-France. En revanche, je me suis heurtée à quelques difficultés. En effet, les résultats attendus ne s'affichent pas sur Datawrapper. Par conséquent, j’ai utilisé OpenRefine pour plusieurs raisons. (ou j’ai eu recours à OpenRefine pour plusieurs raisons) :
- Avant le nettoyage des données : dans la colonne consacrée aux coordonnées géographiques, la latitude ainsi que la longitude sont rassemblées sur une seule colonne, dont séparées uniquement par une virgule. En utilisant l’outil Opendatasoft, je n’ai pas rencontré de soucis. En revanche, lorsque j’ai voulu utilisé Datawrapper pour éditer une carte, toutes les informations importées à partir du fichier CSV n’ont pas été prises en compte. Par conséquent, il serait préférable de nettoyer les données. 

Sur OpenRefine, j’ai procédé à quelques modifications. J’ai dû : 
- Réconcilier les noms de stations franciliennes desservies par le réseau RATP, qui possèdent des toilettes publiques (en les considérant comme des stations ferroviaires).  A la fin, toutes ont une propriété Wikidata attribuée. 
- Renommer les noms des colonnes, en évitant des espaces. 
- Diviser en plusieurs colonnes la colonne coord_geo transformée en deux dont : 
  - Une colonne rassemble les latitudes
  - Une autre colonne rassemble les longitudes
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

Après cette modification, j’ai téléchargé le fichier en format CSV. Cette carte provient du fichier nettoyé à l’aide d’OpenRefine, téléchargé en format CSV et importé dans Datawrapper. 

   * b. Les stations équipées des toilettes publiques

Ce graphique représente le nombre de toilettes publiques par ligne RATP. Notamment, le RER A possède plus de 21 toilettes publiques. En effet, le RER A fait partie des lignes principales en Ile de France. Elle est empruntée par des millions de voyageurs, que ce soit par les touristes ou par les travailleurs. Ensuite, le RER B possède 11 toilettes publiques.
Du côté du métro parisien, six lignes possèdent chacune une toilette publique chacune, comme les lignes 1, 5, 6, 7, 10 et 12. 
Nous avons repéré certaines stations qui possèdent autant de toilettes publiques. Voici les exemples :
- Les stations Charles de Gaulle-Etoile (lignes 1 et RER A) et Châtelet-les-Halles (RER A) possèdent trois toilettes publiques. Cela est dû aux multiples correspondances avec les lignes de métro. Pour les personnes pressées ou pour celles qui n’ont pas de jetons, ces toilettes leur sont bénéfiques. Cela leur évite de rentrer dans les toilettes des centres commerciaux (notamment au Forum des Halles pour la station Châtelet) puisqu’elles sont payantes. 
- La station Noisy Le Grand-Mont d’Est possède deux toilettes publiques. 
- La station Gare de Lyon possède deux toilettes publiques. 
- La station Saint-Germain-en-Laye possède deux toilettes publiques. Celles-ci sont proches d’un site touristique, comme le château et le parc par exemple.  


<iframe src="https://data.opendatasoft.com/chart/embed/toilettespubliques_ratp_graphique/?&static=false&datasetcard=false" width="600" height="450" frameborder="0"></iframe>
Source : OpenDatasoft 
(https://data.opendatasoft.com/chart/embed/toilettespubliques_ratp_graphique/)



2. Les toilettes publiques gratuites et payantes




3. L’accès aux toilettes publiques sur le réseau RATP
   * a. Pour les personnes à mobilité réduite (PMR)




   * b. En zone contrôlée et en hors zone contrôlée 


