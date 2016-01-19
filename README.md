# tp-app-poo
mise en cache du site web

ceci est un tp don l'ennoncé est ici

Cette activité vous proposera d’apporter une amélioration au projet que nous avons créé durant cette partie. Afin d’être sûrs que vous travaillez tous à partir du même code, je vous propose de télécharger la version développée dans le cours : Sources_TP_App.zip. 

Votre mission

Vous allez ici créer un système de mise en cache. Un tel système consiste à stocker certaines ressources nécessitant une phase de traitement plus ou moins longue dans différents fichiers afin de les récupérer beaucoup plus rapidement par la suite. Ce genre de fichiers contient une date d’expiration, date à partir de laquelle le fichier doit être supprimé puis de nouveau généré si on souhaite s’en servir.

Vous allez devoir pouvoir mettre en cache deux types de ressources : des données (comme une news ou une liste de commentaires) ainsi que des vues. Pour parvenir à ce résultat, vous devrez ajouter une nouvelle classe à la bilbiothèque OCFram.

Mise en cache des données

Les données à mettre en cache devront être sérialisées afin de les écrire dans un fichier. Un tel fichier sera composé de 2 parties :
1.Le timestamp correspondant à la date d’expiration.
2.Les données sérialisées.

Ces fichiers seront stockés dans le dossier /tmp/cache/datas. Vous serez libres de choisir le nom de ces fichiers.

Mise en cache des vues

Vous suivrez le même principe que pour la mise en cache des données, à une petite différence près. La première ligne du fichier contiendra le timestamp correspondant à la date d’expiration, et la suite du fichier correspondra au texte généré par la vue (c’est-à-dire le code HTML). Il ne doit pas rester de PHP. Ces fichiers seront stockés dans le dossier /tmp/cache/views. Chaque fichier aura pour nom Nomdelapplication_Nomdumodule_nomdelavue. Si la vue correspondant à l’action à exécuter est en cache, alors le contrôleur correspondant ne doit pas être exécuté. Vous devrez ainsi passer directement la vue en cache à l’objet représentant la page, nécessitant ainsi quelques modifications de la classe correspondante.

La mise en cache des vues nécessite une modification de la façon dont l’application renvoie la réponse au client. Vous devrez faire en sorte de pouvoir obtenir la vue générée par l’objet qui en a la charge afin de la mettre en cache. Ce ne sera ainsi plus la classe gérant la réponse à envoyer au client qui générera la page : vous devrez la générer en dehors puis lui envoyer afin qu’elle l’envoie à son tour au client. Vous apporterez ensuite les modifications nécessaires aux codes affectés par ces changements.

Afin de savoir quelles vues sont à mettre en cache, chaque contrôleur pourra implémenter une méthode createCache() renvoyant un tableau de la forme ['nomdelavue' => 'duree']. Pour la durée, libre à vous de l’exprimer comme vous le souhaitez. Si vous êtes à court d’idées, je vous propose de regarder du côté des formats relatifs que vous pouvez utiliser conjointement avec DateInterval::createFromDateString afin de déduire le timestamp auquel le fichier cache devra être détruit. 

Objectif

Vous devrez mettre en cache plusieurs parties du site :
•La vue correspondant à la page d’accueil du site.
•Chacune des news.
•Toutes les listes de commentaires (une liste de commentaires correspond à l’ensemble des commentaires liés à une news).

La mise en cache des news et commentaires ne se fait pas dès leurs créations mais dès qu’ils sont récupérés pour la première fois. Vous devrez par ailleurs penser à supprimer les ressources mises en cache qu’il faut lorsqu’une news ou un commentaire est ajouté, modifié ou supprimé.

Votre travail sera évalué selon les critères suivants. 
•La lisibilité du code : veillez à produire un code clair pour celui qui vous corrigera.
•Le respect du principe d’encapsulation.
•La création d’une classe gérant le cache : la gestion du cache doit se faire grâce à une instance d’une classe que vous créerez au sein de la bibliothèque.
•Le fonctionnement du système : toutes les données et vues suscitées doivent être mises en cache.
•La suppression automatique des ressources en cache : si une ressource périmée est lue dans le cache, alors celle-ci doit automatiquement être supprimée.
•La suppression manuelle des ressources en cache : si des ajouts, modification ou suppression ont été apportés, alors les ressources concernées doivent être supprimées du cache

