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
Grace à metrics (outil d'analyse ) on constate que le projet est couvert en documentation à 80%  

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







