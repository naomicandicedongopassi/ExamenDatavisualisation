# 4L9IF0P3 - Analyse des données et datavisualisation 

## **Les toilettes publiques sur les lignes RATP en Ile-de-France**
 
Mon étude porte sur les toilettes publiques sur les lignes RATP en Ile de France. Bien que les transports ferroviaires soient les plus plébiscités par les Franciliens et par les touristes étrangers et provinciaux pour se rendre à la capitale, je remarque que la plupart des toilettes publiques sont situées dans les grandes gares parisiennes telles que Paris Montparnasse, Paris Saint-Lazare, Paris Est, Paris Nord, Paris Austerlitz, Paris Gare de Lyon, Paris Bercy. De plus, concernant les stations parisiennes et franciliennes desservies par le réseau RATP, j’ai rarement vu des toilettes publiques. 
C’est la raison pour laquelle, j’ai choisi de mener cette étude afin de mettre en évidence leur implantation ainsi que les conditions d’utilisation des toilettes publiques dans les stations parisiennes. 

> Sommaire 

1. Le nombre de toilettes publiques 
   * a. Par lignes RATP (métro et RER) 
   * b. Les stations équipées des toilettes publiques 

2. Les toilettes publiques gratuites et payantes

3. L’accès aux toilettes publiques 
   * a. Pour les personnes à mobilité réduite
   * b. Par le biais du ticket T+ et le pass Navigo


___________________________________________________________



1. Le nombre de toilettes publiques
   * a. Par lignes RATP (métro et RER) 

Ce graphique représente le nombre de toilettes publiques par ligne RATP. Notamment, le RER A possède plus de 21 toilettes publiques. En effet, le RER A fait partie des lignes principales en Ile de France. Elle est empruntée par des millions de voyageurs, que ce soit par les touristes ou par les travailleurs. ---

<iframe src="https://data.opendatasoft.com/chart/embed/toilettespubliques_ratp_graphique/?&static=false&datasetcard=true" width="600" height="450" frameborder="0"></iframe>



   * b. Les stations équipées des toilettes publiques



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
