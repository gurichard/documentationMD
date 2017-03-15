Introduction à l'utilisation d'imi-admin
----------------------------------------
Depuis la version **0.27.0** d'iv-middleware-server, les commandes disponibles depuis le script de service tel que *reload*, *kick_user*, *delogall*, *enable_log_levels* et *disable_log_levels* ont été déplacer sur un outil séparer pour des raisons de sécurités. Ainsi la commande *disable_log_levels* ne se trouve plus au même niveau que la commande *restart*. Il n'est normalement plus possible de *restart* le serveur par erreur via un <kbd>Ctrl+r</kbd> malvenu.

Prérequis et changements
------------------------
#### Package devenu obsolète
- socat

#### Packages nécessaires
- python2.6
- python-argparse

#### Élément nécessaire
- une socket unix, utilisable uniquement par un utilisateur root, actuellement fournie par iv-middleware-server.

Utilisation générale
--------------------
imi-admin est équipé d'une aide interactive permettant d'accéder à l’ensemble des commandes et de leur aide.

- Pour accéder à l'aide générale du script, donnant la définition des différentes commandes:
```
imi-admin -h
```

Gestion du provisioning et de la configuration
----------------------------------------------
#### Vérification de la configuration d'iv-middleware-server
imi-admin a une commande permettant de vérifier la syntaxe de la configuration complète du serveur middleware. A chaque erreur détectée, la vérification échouera et donnera l'option et le couple marque blanche / projet incriminé.

- Pour accéder à l'aide de **check_config**, donnant la définition de la commande:
```
imi-admin check_config -h
```

- Usage
```
imi-admin check_config
```

#### Rechargement de la configuration complète
imi-admin a une commande permettant de recharger l'**ensemble** de la configuration du middleware (ivmid.ini + middleware.conf.d/*.ini) et d'ajouter les nouveaux projets ou de mettre à jour ceux qui ont été modifié.

- Pour accéder à l'aide de **reload**, donnant la définition de la commande:
```
imi-admin reload -h
```

- Usage
```
imi-admin reload
```

**Attention:** A chaque **reload**, un **check_config** est lancé, s'il échoue le rechargement de la configuration est avorté.

#### Chargement d'un projet unitaire
imi-admin a une commande permettant de charger la configuration d'un projet ciblé et de l'ajouter ou de le modifier.

- Pour accéder à l'aide de **load**, donnant la définition de la commande:
```
imi-admin load -h
```

- Usage
```
imi-admin load -w WHITELABEL -p PROJECT
```

**Attention:** A chaque **load**, un **check_config** est lancé, s'il échoue le chargement du projet est avorté.

#### Déchargement d'un projet unitaire
imi-admin a une commande permettant de décharger un projet ciblé du middleware.

- Pour accéder à l'aide de **unload**, donnant la définition de la commande:
```
imi-admin unload -h
```

- Usage
```
imi-admin unload -w WHITELABEL -p PROJECT
```

**Attention:** A chaque **unload**, une vérification de sécurité est faite sur le projet ciblé, si des agents sont encore connectés, le déchargement est avorté, invitant à déconnecter ceux ci.

Gestion des utilisateurs
------------------------
#### Déconnecter un utilisateur distant
imi-admin a une commande permettant de déconnecter un utilisateur sur le middleware sur un projet cible.

- Pour accéder à l'aide de **kick_user**, donnant la définition de la commande:
```
imi-admin kick_user -h
```

- Usage
```
imi-admin kick_user -w WHITELABEL -p PROJECT -u USERNAME
```

**Attention:** Si un agent est ciblé celui ci sera déconnecté, si un agent superviseur ou superviseur est ciblé le superviseur et son agent superviseur seront déconnectés.

#### Déconnecter les utilisateurs d'un ou plusieurs projets
imi-admin a une commande permettant de déconnecter l'ensemble des **agents** sur l'ensemble des projets, sur une marque blanche ciblée ou une un projet en particulier.

- Pour accéder à l'aide de **delogall**, donnant la définition de la commande:
```
imi-admin delogall -h
```

- Usage
```
imi-admin delogall [-w WHITELABEL] [-p PROJECT]
```

**Attention:** La commande de **delogall** utilise un événement associé à l'utilisateur consistent. Si le middleware n'a pas la main sur l'utilisateur consistent il ne peut pas faire le **delogall**, pour contrer cela, l'utilisateur consistent peut être déconnecter de force (via un client explorer) afin de laisser le middleware reprendre la main dessus, ce fonctionnement opère automatiquement si le login de l'utilisateur consistent échoue avec pour raison: *Utilisateur déjà connecté*

Gestion des indicateurs
-----------------------
#### Purger les indicateurs vocaux
imi-admin a une commande permettant de purger et de reprendre les nouvelles valeurs des indicateurs vocaux depuis le serveur dispatch sur l'ensemble des projets, sur une marque blanche ciblée ou une un projet en particulier.

- Pour accéder à l'aide de **flush_indicators**, donnant la définition de la commande:
```
imi-admin flush_indicators -h
```

- Usage
```
imi-admin flush_indicators [-w WHITELABEL] [-p PROJECT]
```

Gestion des traces
--------------------------
#### Activation des niveaux de traces dans les logs
imi-admin a une commande permettant d'activer un niveau de trace sur les logs du middleware.

- Pour accéder à l'aide de **enable_log_levels**, donnant la définition de la commande:
```
imi-admin enable_log_levels -h
```

- Usage
```
imi-admin enable_log_levels [levels...]
```

**Note:** Niveaux de logs disponibles => DEBUG, INFO, ERROR, WARN.

#### Désactivation des niveaux de traces dans les logs
imi-admin a une commande permettant de désactiver un niveau de trace sur les logs du middleware.

- Pour accéder à l'aide de **disable_log_levels**, donnant la définition de la commande:
```
imi-admin disable_log_levels -h
```

**Note:** Niveaux de logs disponibles => DEBUG, INFO, ERROR, WARN.