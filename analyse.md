gaspar henniaux
loïcia robart

# Présentation globale du projet

## Utilité du projet

* GSON est une bibliothèque Java utilisée pour convertir des objets Java en leur représentation JSON
et vice versa. Très pratique pour stocker les données de manière structurée et légère.  


* Le projet est utilisé en étant importé dans un projet java, 
attention, sous maven la dépendance devra être ajouté au fichier pom.xml.
Ensuite, il suffit d'importer la bibliothèque dans le fichier java où on souhaite l'utiliser.
On crée un objet Gson (new Gson()) et on peut utiliser les methodes toJson(obj java) et fromJson(obj json, class java) 
pour convertir les objets.
La sortie, selon la méthode utilisée, sera un objet JSON ou un objet Java. 
On parle de Sérialisation (java to json) et de Désérialisation (json to java).  


## Description du projet  

* Nous pouvons noter la présence d'un readme par module qui survole le contenu de ce dernier.
Le readme principale contient une présentation du projet ainsi que ses objectifs et les manières de l'utiliser ainsi que
des liens vers la documentation.  


* Oui le projet est bien documenté, tout est précisé, pas seulement les parametres et le return.
De plus dans le UserGuide, il y a des exemples d'utilisation de la bibliothèque, avec la classe depuis laquelle tout démarre (Gson)
ainsi que la méthode qui est invoqué en premier.
Grace à metrics (outil d'analyse ) on constate que le projet est couvert en documentation à 80% , il reste à vérifier que celui-ci aide réellement à la 
compréhension des méthodes les plus complexes, et qu'elles ne sont pas juste la pour spécifier les types des paramètres et des returns  
On pourrait ainsi développer la documentation sur certaines méthodes qui ne sont pas explicites et réduire la ou elle encombre plus le code qu'autre chose.

# Présentation globale du projet  

## Analyse du git  

* Depuis le dépot git on peut compter deja plus de 140 contributeurs, non la contribution n'est pas équilibrée, 
certains n'ont travaillé que sur 1 ligne tandis que d'autres sur plus de 150 000 lignes de code.
De même, certains ont été très présents au début mais ne travaillent plus dessus depuis des années, et inversement.
Ainsi, on ne retrouve personne qui est encore actif et qui a suivi l'intégralité du projet.  

* Le projet est toujours actif, des commits sont faits très régulièrement (encore la veille), par le même contributeur. 

* 12 branches sont définies, seules 2 (y compris la main) sont encore actives. Les autres n'ont plus été utilisée depuis plusieurs années.  

* Le processus de pull request est bien utilisé, 868 sont fermées et 100 sont en attente.  

# Architecture logicielle  

## Utilisation de bibliothèques extérieures  

* Nous comptons 3 bibliotheques exterieures qui sont toutes utilisees. Cependant dans certaines classes les imports ne sont pas
justifiés et pourraient donc être supprimés pour avoir un code plus propre et lisible.  

  * Ces 3 bibliothèques font des choses différentes et sont donc justifiés et aucune d'elle ne peut être supprimée.

## Organisation en paquetage

* Nous avons découvert grace a dependency metrics dans intellij que certains packages/classes étaient dépendants les uns des autres 
de façon cyclique. Cela peut engendrer des difficultes de compréhension, et donc repérer les erreurs, cela augmente la difficultés de pouvoir 
isoler certaines fonctionnalités. Cela peut également rendre plus difficile la gestion des tests unitaires et de réfactorisation de code car tout sera lié.  

Il faudrait ainsi minimiser les cycles de dépendances, on peut par exemple imaginer l'utilisation de design pattern qui restructureraient la code.  

* Dans le coeur du projet (le dossier gson) il n'y a aucun paquetage ne contenant qu'un seul paquetage sans aucune classe, cependant nous en avons remarqué quelques uns ayant ce comportement (exemple le paquetage gson/src/main/java-templates), cependant il ne semble pas pertinent de le réfactorer car cette hiérarchie bien que plus lourde est essentiellement structurelle et permet de maintenir une bonne cohérence de code. Cela est aussi positif pour l'extensibilité.

* Pour ce qui est des noms de paquetages -> ils sont relativement intuitifs, ce qui rend le projet accessibles pour des personnes inconnus à celui-ci, cela facilite aussi la recherche de certaines classes ou fonctionnalités ou encore la compréhension des roles des différents paquetages.
Certains d'entre eux nous donnent des infos sur le lien avec la base de donnée ( exemple gson/src/main/java/com.google.gson/internal/sql)
Nonobstant, les paquetages sont souvent nommés selon les fonctionnalités qu'ils implementent (on parle d'organisation métiers ), pas de lien avec les design patterns utilisées ou des modeles de conception partciculiers.

## Répartition des classes dans les paquetages    

* Au total il y a 84 fichiers (commande ds fichier gson/src/main/java/com.google.gson "$find . -type f | wc -l") cela peut être des classes, des enums ou des interfaces.
 Avec un minimum de 1 classe (dans le paquetage gson/src/main/java/internal/bind/util) et un maximum de 30 (gson/src/main/java/com.google.gson), on a une moyenne d'environ 9 classes par paquetage (cependant l'écart type est très grand -> moyenne n'est pas très indicative).

 il serait envisageable de regrouper certaines de ces classes dans de nouveaux sous paquetages pour que le gros paquetage de 30 classes soit moins surchagé. 

* On remarque que une grande majorité des classes de code se trouvent un même paquetage (le paquetage gson/src/main/java/com.google.gson) -> une bonne pratique serait de mieux répartir les nombres de classes dans les paquetages.
 
* Plusieurs paquetages non feuilles contiennent des classes (exemple gson/src/main/java/com.google.gson ou encore gson/src/main/java/internal ou gson/src/main/java/internal/bind) ,cela n'est pas forcément une mauvaise chose et peut permettre de réduire la complexité de la structure, d'offrir des mêmes fonctionnalités à plusieurs sous paquetages. En inconvénient,  cela peut diminuer la cohérence de regroupement des fonctionnalités et créer des dépendances inutiles entre les autres sous paquetages.

* Dans la classes Excluder.java (qui se trouve dans le paquetage internal), on retrouve des imports des paquetages "annotation", "internal.reflect", ou encore "stream".
  
* couplage : Peu de dépendances entre les classes et paquetages est préfèrable pour rendre le projet plus extensible et facilement modifiable car les parties sont plus indépendantes les unes des autres.


## Organisation des classes  

* Après avoir affiché le diagramme uml qui montre les liens d'héritage entre les classes, on remarque une DIT très minime, avec une profondeur maximale de 2 ( TreeTypeAdaptator hérite de SerializationDelegatingTypeAdaptator qui hérite de TypeAdaptator ). On voit qu'il y a un max d'enfants de 9 pour les enfants de TypeAdaptator et un min de 1 (exemple l'enfant de la classe JsonWriter).

* A part pour la classe type Adapatator qui a 9 enfants, sinon on retrouve très peu d'héritage de classe, et celle-ci est donc plutot plate avec une profondeur maximum de 2.

* Une hiérarchie aussi plate participe ainsi au fait qu'il y ait moins de couplage entre les différentes parties du code. Plus une classe a un couplage faible plus elle est considérée comme stable, la dépendance de cette classe avec les autres est minimale.
  
* On peut ainsi facilimer modifier le code d'une classe sans que cela impacte les autres.  
  
* Cela rend également les tests plus faciles, avec la créations de tests unitaires independants les uns des autres.

* Avec un couplage plus faible le projet est plus compréhensible, chaque classe a une responsabilité claire et on peut plus facilement réutiliser les différentes parties de code.






attention : 
methodes publiques dans methodes privées
probleme nom methodes att (exemple convention majuscules att statiques tt ca)
couverture test
couverture docs 
code commentée ?
methodes mal commentes qu'on comprend pas
readme peut etre developpee
nom des methodes/classes/packages pas explicites
nombres magiques 
noms de variables pas explicites
classe trop grande
