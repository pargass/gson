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

* Enfin nous avons remarqué que les classes exceptions ne se trouvaient pas dans un paquetage spécifiques mais avec toutes les autres classes du projet.

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

# Analyse approfondie

## Tests 

* pour compter les classes de test : /IdeaProjects/gson/gson/src/test`$ find . -type f -name "*Test.java" -o -name "*Tests.java" | wc -l`
il y a 112 classes de test, ce qui est un nombre conséquent et qui montre que le projet est bien testé.

* pour compter les tests : /IdeaProjects/gson/gson/src/test`$ find . -type f -name "*Test.java" -o -name "*Tests.java" | xargs grep -o '@Test' | wc -l`
il y a 1332 tests.

* pour compter les assertions : /IdeaProjects/gson/gson/src/test`$ find . -type f -name "*Test.java" -o -name "*Tests.java" | xargs grep -E 'assertThat|assertEquals|assertTrue|assertNotNull|assertThrows|fail' | wc -l`
il y a 3372 assertions.

* chaque test compte en moyenne environ 2.53 assertions -> ce qui semble être bien car cela signifie qu'il y a possiblement plusieurs post conditions qui sont testées à chaqeu fois.

 On remarque que presque toutes les assertions sont des assertThat, il pourrait être enviseageable de les diversifier.  
 
* la grande majorité des tests sont des tests unitaires -> bonne pratique, chaque fonctionnalité est testée
* Tous les tests du projet passent avec succès  


## Commentaires

* On peut remarquer qu'il existe du code commenté qui pourrait donc être supprimé pour nettoyer le projet de lignes inutiles -> par exemple à la classe TypeAdapter : ligne 250 à 290 (à supprimer) et TypeAdapterFactory : partout (à supprimer)
  
* Il y a également parfois certains commentaires qui ne sont pas necessaires et qui reprennent simplement le nom de l'attribut. Par exemple dans la classe stream.JsonReader.java ligne 278 (peekedNumberLenght).

* Il y a environ 1600 lignes de codes de commentaire ( trouvée avec la ligne de commande : `$ find . -name "*.java" -print0 | xargs -0 grep -E '^\s*//|^\s*/\*|^\s*\*/' | wc -l`)

* Le projet est très commenté en général et il est difficile de trouver une seule méthode qui n'est pas expliqué en commentaire. Certaines parties plus techniques pourraient cependant mieux détaillé pour qu'une personne extérieure au projet comprennent encore plus facilement.

## Dépréciation  
  
* il y a une méthode dépréciée dans la classe JsonWriter à la ligne 312, setLenint(). Elle est appelée uniquement par une méthode de test. Il est préférable de remplacer les appels à cette méthode par la méthode setStrictness() ce qui est préconisé par la documentation.

* utiliser du code déprécié peut entrainer des erreurs dans le futur, des problèmes de sécurité, de maintenance et de performance. Il est judicieux de remplacer des appels à des méthodes dépréciées par des méthodes plus récentes.

## Dupplication de code  

* Quand on inspecte le code duppliqué dans intellij avec Analyse, on ne récupère que des "weak warnings", et quand on va regarder en détail on ne se retrouve pas réellement avec des lignes de codes duppliquées qui peuvent être supprimées. Nous en avons conclus que sur ce point là il ne semblait pas y avoir de grosses corrections possibles.

## God classes  

 *  la classe Gson est une classe sur laquelle nous nous sommes penchés. c'est une classe qui contient plus de 1500 lignes de code, plus de 40 importations et plus de 30 méthodes. dans un premier temps nous avons pensé qu'il s'agissait d'une god class, mais après analyse, nous avons constaté que la classe était bien structurée et ne gérait pas trop de responsabilités. Elle s'occupe de la sérialisation et de la désérialisation de données. Les imports nombreux sont nécessaires pour la gestion des exceptions et des types de données.
   
 *  Une god class est identifiable par plusieurs critères : elle contient beaucoup de lignes de code, et beaucoup de dépendances. Elle gère beaucoup de responsabilités. Ce sont généralement des classes qui sont difficiles à maintenir et à comprendre.
   

* la présence d'une god class entraine des problèmes de maintenance, si elle contien beaucoup de responsabilités, il est difficile de la modifier sans impacter le reste du code et la réutilisation de cette classe est difficile car si on ne veut utiliser qu'une partie de ses fonctionnalités, on doit quand même importer toutes les dépendances, même celles qui ne nous intéressent pas. Le travail en équipe est également compliqué car il est difficile de travailler sur une classe qui contient beaucoup de responsabilités sans impacter le travail des autres.


## Analyse des méthodes  

* la complexité cyclomatique d'une méthode est un indicateur de la complexité de la méthode. Plus la complexité cyclomatique est élevée, plus la méthode est complexe. Il est préférable de réduire la complexité cyclomatique des méthodes pour les rendre plus lisibles et plus maintenables. entre 1 et 10 la complexité est considérée comme bonne et au dessus de 10, il est préférable de réduire la complexité de la méthode.

* nous avons trouver une méthode dans la classe stream.JsonReader, doPeek() qui a une complexité cyclomatique de 80. Cela s'explique par le fait que la méthode contient beaucoup de conditions imbriquées (if, else if, else, switch, case). Nous avons trouvé d'autres méthodes avec une complexité cyclomatique élevée dans cette classe comme peekNumber() qui a une complexité cyclomatique de 85 ...


* il y a plein de manière de réduire la complexité cyclomatique d'une méthode, par exemple en divisant la méthode en plusieurs méthodes plus petites, en enlevant les imbrications de conditions, en appliquant le principe de responsabilité unique, en utilisant certains design patterns comme le pattern stratégie ou le pattern état etc.

* Concernant la longueur des méthodes, plus une méthode est longue, plus elle est difficile à comprendre et à maintenir. Encore une fois, il serait préférable de diviser ces méthodes en plusieurs méthodes. Nous pouvons reprendre l'exemple de la méthode doPeek() qui contient environ 100 lignes de code.
  
* Pour ce qui est du nombre de paramètres, on peut considérer qu'à partir de 4-5 cela peut commence à faire trop. En effet, la méthode peut devenir difficile à comprendre, et cela peut signifier que celle-ci gère trop de responsabilité (contraire au principe de responsabilité unique).

* Dans le projet on retrouve notamment dans la classe ReflectiveTypeAdaptaterFactory, la méthode "createBoundField" qui recquiert 7 arguments. Sinon le maximum dans le projet reste de 5 paramètre et cela concerne 2 methodes seulement ( getBoundField dans la classe ReflectiveTypeAdaptaterFactory ou getTypeAdaptater dans la classe JsonAdaptaterAnnotationTypeAdaptaterDactory).

* Pour réduire ce nombre on peu envisager de diviser la méthode en plus petites méthodes, d'utiliser des variables de classe si ccela est possible ou encore de se tourner vers un design différent.
  
* avoir des méthodes qui à la fois modifient l'état de l'objet et qui retournent des informations est une mauvaise pratique. Il est préférable de séparer ces deux types de méthodes car c'est un principe de command query separation.

* c'est une mauvaise pratique car une méthode ne devrait faire qu'une seule chose. ce sont des methodes plus difficiles à tester et à maintenir et plus difficiles à réutiliser.

* Une méthode qui renvoie un code d'erreur n'est en général pas une bonne pratique, sauf si celle ci a bien documentée la valeur de retour. Sinon cela rend la maintenance plus difficile, le code est plus diffcile à comprendre, on ne gère pas forcement les traitement des erreurs et on se retrouve avec des nombres magiques.

* on peut citer dans le projet la méthode nextNonWhitespace() dans la classe stream.JsonReader à la ligne 1445. Celle-ci renvoie la valeur -1.

* Pour corriger cela on pourrait par exemple utiliser des exceptions ou être sur d'avoir une bonne gestion d'erreurs cohérente et compréhesible.


# Nettoyage de Code et Code smells  

## Règle de nommage   

* Le projet utilise des bons noms partout qui définissent toujours la fonctionnalité de la méthode -> exemples (isCapturingTypeVariablesForbidden dans la classe TYpeToken ou encore excludeFieldsWithModifiers dans la classe GsonBuilder), nous n'en avons pas trouvé à modifier.

## Nombre magique  

* Nous avons pu trouver des nombres magique dans le code par exemple : JsonPrimitive : ligne 260, 265, 269. Cela augmente les risques d'erreur (faute de frappe par exemple), le code est plus difficile à tester et il est moins clair à comprendre ( on ne sait pas à quoi correspondent les valeurs )
  
* Ces nombre pourraient être remplacées par des constantes initialisées au début de la classe.

## Structure du code  
  
* Dans le package java.com.google.gson.internal.sql, on retrouve beaucoup de problèmes en terme de structure de code. Pour en citer quelques-uns, dans la classe LinkedTreeMap ligne 448 et 449, on retrouve deux attributs privés entre deux méthodes publiques de la classe (entrySet et keySet). On a également dans une majorité des classes de ce package comme LazilyParsedNUmber (ligne 40 asBigDecimal) ou LinkedTreeMap (ligne 424 rotateRight) , les méthodes privées qui sont entremélées entre les méthodes publique.

* Cela nuit à la lisibilité du code, la maintenabilité et le compréhension, car la structure n'est pas claire et cohérente partout. IL serait préférable de regrouper les définition d'attributs en début de classe, et les méthodes privées en fin de classe.
  
## Code mort  

* Nous avons pu trouver du code mort : la fonction "excluder" à la ligne 417 de la classe Gson.Java , celle-ci n'est appelé nulle part et pourrait donc être supprimée afin de nettoyer encore plus le code et le rendre plus lisible. De plus il est Deprecated (obsolète), raison de plus pour le supprimer. Celui-ci est testé.

* Pour en citer d'autres, on trouve dans la classes internal.sql.GsonTypes de nombreuses méthodes comme toString ligne 569 et une autre ligne 675 ou encore hashCode ligne 669 qui ne sont pas appelés nul part. Il y a également la méthode JavaVersion dans la classse internal.sql.JavaVersion qui n'implémente aucun code et qui n'est appelé nul part. Il faut faire attention pour voir si ils sont supprimables qu'ils ne soient pas la parce  que la classe implémente une interface et doit les redéfinir. Cependant dans les redéfinitions de méthodes obligatoires mais jamais appelées en internes, certaines implémente des lignes de codes non necéssaires puisque jamais appelé.

* Il faut également nettoyer les tests si on supprime des bouts de code.
* Enlever tous ces morceaux de code mort permettra de réduire la taille du code et ainsi le rendre plus lisible et compréhensible, cela permet également de réduire sur des gros projets les temps de compilation.



