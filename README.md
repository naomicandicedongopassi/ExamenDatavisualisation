# 4L9IF0P3 - Analyse des données et datavisualisation 

## **Les toilettes publiques sur le réseau RATP en Ile-de-France**
 
Mon étude porte sur les toilettes publiques sur les lignes RATP (régie autonome des transports parisiens) en Ile-de-France. Bien que les transports ferroviaires soient les plus plébiscités par les Franciliens et par les touristes étrangers et provinciaux pour se rendre à la capitale, je remarque que la plupart des toilettes publiques sont situées dans les grandes gares parisiennes telles que Paris Montparnasse, Paris Saint-Lazare, Paris Est, Paris Nord, Paris Austerlitz, Paris Gare de Lyon, Paris Bercy. De plus, la plupart d’entre elles sont payantes. Puis, concernant les stations parisiennes et franciliennes desservies par le réseau RATP, j’ai rarement vu des toilettes publiques. 
C’est la raison pour laquelle, j’ai choisi de mener cette étude afin de mettre en évidence leur implantation ainsi que les conditions d’utilisation des toilettes publiques dans les stations parisiennes. 


> Sommaire 

1. Le nombre de toilettes publiques 
   * a. Généralités
   * b. Les stations équipées des toilettes publiques 

2. Les toilettes publiques gratuites et payantes

3. L’accès aux toilettes publiques 
   * a. Pour les personnes à mobilité réduite
   * b. Par le biais du ticket T+ et le pass Navigo


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

Après cette modification, j’ai téléchargé le fichier en format CSV. Cette carte provient du fichier nettoyé à l’aide d’OpenRefine, téléchargé en format CSV et importé dans Datawrapper. 

   * b. Les stations équipées des toilettes publiques


<iframe src="https://data.opendatasoft.com/chart/embed/toilettespubliques_ratp_graphique/?&static=false&datasetcard=false" width="600" height="450" frameborder="0"></iframe>


