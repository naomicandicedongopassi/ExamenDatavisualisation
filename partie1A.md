Partie 1 : Le nombre de toilettes publiques sur les lignes RATP

   * a. Généralités 

Cette carte représente le nombre de stations RATP qui possèdent des toilettes publiques en Ile-de-France. Grâce aux coordonnées géographiques, la plupart d’entre elles sont situées dans Paris, grâce aux métros parisiens. Les autres sont situées dans la région parisienne par le biais des autres lignes RATP. 

<div class="flourish-embed flourish-map" data-src="visualisation/8573833"><script src="https://public.flourish.studio/resources/embed.js"></script></div>

Pour connaître la localisation des toilettes publiques RATP en Ile-de-France, j’ai voulu utiliser Flourish, à partir du fichier Excel téléchargé sur le site Open Data RATP. En revanche, je me suis heurtée à quelques difficultés. En effet, les résultats attendus ne s'affichent pas sur Flourish. Par conséquent, j’ai utilisé OpenRefine pour la raison suivante :
- Avant le nettoyage des données : dans la colonne consacrée aux coordonnées géographiques, la latitude ainsi que la longitude sont rassemblées sur une seule colonne, dont séparées uniquement par une virgule. En utilisant l’outil Opendatasoft, je n’ai pas rencontré de soucis. En revanche, lorsque j’ai voulu utilisé Flourish pour éditer une carte, toutes les informations importées à partir des fichiers Excel ou du fichier CSV n’ont pas été prises en compte. Par conséquent, il a fallu procéder au *datawrangling* (ou nettoyage des données). 

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
 

* [Page suivante](partie1B.md) 
* [Retour à la page d'accueil](README.md) 
