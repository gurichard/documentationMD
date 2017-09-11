Introduction à l'utilisation d'iap-admin
----------------------------------------
Depuis la version **0.0.0** d'iv-api-server, les commandes de services tel que *enable_log_levels* et *disable_log_levels* ont été déplacé sur un outil séparer pour des raisons de sécurités.
Ainsi la commande *disable_log_levels* ne se trouve plus au même niveau que la commande *restart*. Il n'est normalement plus possible de *restart* le serveur par erreur via un <kbd>Ctrl+r</kbd> malvenu.
De plus certain scripts ont été intégré directement dans l'outil tel que:
*sideload_apikeys*, *create_mail_entrypoint*, *db_migrate*, *clear_webadmin_infos*, *purge_records*

Prérequis et changements
------------------------
#### Package devenu obsolète
- socat

#### Packages nécessaires
- python2.6
- python-argparse

#### Élément nécessaire
- une socket unix, utilisable uniquement par un utilisateur root, actuellement fournie par iv-api-server.

Utilisation générale
--------------------
iap-admin est équipé d'une aide interactive permettant d'accéder à l’ensemble des commandes et de leur aide.

- Pour accéder à l'aide générale du script, donnant la définition des différentes commandes:
```
iap-admin -h
```

Création des sideload apikeys
-----------------------------
Au lieu d'écrire la query dans la console, l'insert directement en bdd.

- Pour accéder à l'aide de **sideload_apikeys**, donnant la définition de la commande:
```
iap-admin sideload_apikeys -h
```

- Usage
```
iap-admin sideload_apikeys [-p CONFIG_PATH] [-c MODULES_CONFIG_PATH] file
```

**Attention:** Solicite très peu le serveur en lui même. Risque minimal.

DB Migrate
----------
Fonctionne comme l'ancien script. Va mettre à jour le schéma de base de données des API concernés.

- Pour accéder à l'aide de **db_migrate**, donnant la définition de la commande:
```
iap-admin db_migrate -h
```

- Usage
```
iap-admin apiserver_db_migrate [-p CONFIG_PATH] [-c MODULES_CONFIG_PATH] [configapi,eventsapi ...]
```

**Attention:** Ne doit être fait que lors d'une install ou une mise à jour.Solicite très peu le serveur en lui même. Risque minimal.

Création d'un point d'entrée mail
---------------------------------
Fonctionne comme l'ancien script.

- Pour accéder à l'aide de **create_mail_entrypoint**, donnant la définition de la commande:
```
iap-admin create_mail_entrypoint -h
```

- Usage
```
iap-admin create_mail_entrypoint [-c CONFIG_PATH] -p PROJECT -w WHITELABEL -e ENTRYPOINTS [ENTRYPOINTS ...]
```

**Attention:** Ne doit être fait que lors d'une install ou une mise à jour.Solicite très peu le serveur en lui même. Risque minimal.

Nettoyage du cache de les infos des webadmins
---------------------------------------------
iap-admin a une commande permettant de vider le cache des informations relatives aux webadmins déjà contacter par le deploymentAPI. A chaque appel API nessitant de connaitre les informations d'un node webadmin, un cache va etre sollicité, si le cache a les informations du node concerné il les donne sinon il utilise le deploymentAPI afin de les récupérer.

- Pour accéder à l'aide de **clear_webadmin_infos**, donnant la définition de la commande:
```
iap-admin clear_webadmin_infos -h
```
- Usage
```
iap-admin clear_webadmin_infos -p PROJECT -w WHITELABEL
```

**Attention:** Le vidage du cache en lui même ne représente aucune charge pour le serveur, mais cela va soliciter le deploymentAPI.

Purge des records
-----------------
iap-admin a une commande permettant de déclencher une purge des records sur l'api-server.

- Pour accéder à l'aide de **purge_records**, donnant la définition de la commande:
```
iap-admin purge_records -h
```

- Usage
```
iap-admin purge_records [-a] [-w WHITELABEL] [-p PROJECT] [-c CONFIG_PATH]
```

**Attention:** Cette commande représente un risque important pour le serveur, car cela solicite le disque du serveur et MySQL. Plus un projet a de records à purger, plus la base de donnée est solicité et les fichiers seront nombreux à être supprimer. A utiliser en periode creuse.

**Note:** La commande n'a pas d'actions par défault, soit on spécifie un whitelabel / project soit on spécifie -a (--all).

Gestion des traces
--------------------------
#### Activation des niveaux de traces dans les logs
iap-admin a une commande permettant d'activer un niveau de trace sur les logs du api-server.

- Pour accéder à l'aide de **enable_log_levels**, donnant la définition de la commande:
```
iap-admin enable_log_levels -h
```

- Usage
```
iap-admin enable_log_levels [levels...]
```

**Attention:** L'activation de nombreux niveaux de trace va faire gonfler la taille des logs, en dehors de cela, l'activation en elle même ne représente pas de risque pour le serveur.

**Note:** Niveaux de logs disponibles => DEBUG, INFO, ERROR, WARN.

#### Désactivation des niveaux de traces dans les logs
iap-admin a une commande permettant de désactiver un niveau de trace sur les logs du api-server.

- Pour accéder à l'aide de **disable_log_levels**, donnant la définition de la commande:
```
iap-admin disable_log_levels -h
```

**Attention:** La désactivation de nombreux niveaux de trace va alléger la taille des logs, en dehors de cela, la désactivation en elle même ne représente pas de risque pour le serveur.

**Note:** Niveaux de logs disponibles => DEBUG, INFO, ERROR, WARN.
