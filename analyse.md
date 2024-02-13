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






attention : 
couverture test
couverture docs 
code commentée ?
methodes mal commentes qu'on comprend pas
readme peut etre developpee
nom des methodes/classes/packages pas explicites
nombres magiques 
noms de variables pas explicites
classe trop grande
