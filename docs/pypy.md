# RPMisation de pypy et du middleware
Afin de rendre accessible pypy en tant que rpm il est nécessaire de:

## Fournir pypy
Afin de fournir pypy, idéalement, il faudrait pouvoir le compiler pour une architecture cible.
Il est néanmoins possible de télécharger une archive contenant une version pré-compilée, toutefois le gain est bien moindre que si on le compiler.
Ne pas oublier de faire un lien vers le binaire afin de l'appeller comme python dans la console.

## Fournir une base à pypy
Il est nécessaire d'installer pip afin de faciliter l'installation des packages et des differents socles.
Pour ce faire, il est envisageable de fournir un rpm executant un script faisant tout simplement ceci.

- Installer pip
pypy -m ensurepip 
- Installation de setuptools, wheel et mise à jour de pip
/opt/pypy/bin/pip install -U pip wheel setuptools

## Fournir les prérequis à twisted & autres packages
Tout cela est possible via une installation par pip 
/opt/pypy/bin/pip install pyOpenSSL service_identity demjson hashids python-dateutil
/opt/pypy/bin/pip install twisted==16.0.0

## Fournir les packages prérequis à iv-middleware-server
Packages nécéssaires:
- iv-commons
- iv-cccp
- txsocksjs /!\ Ne pas oublier la branche spéciale pour pypy
- trest
- plague
- ivprotocols

A installer via un pypy setup.py install

# Fournir iv-middleware-server
Package nécéssaire:
- iv-middleware-server

A installer via un pypy setup.py install
