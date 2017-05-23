# Etat actuel
L'annuaire est chargé à la demande par le bandeau qui fait une demande au serveur middleware. Celui ci va utiliser une API du webadmin afin de recupérer un JSON contenant les agents, superviseurs, files et contacts du profile de l'agent.
Ce JSON a pour structure:
```
{
    agents : {key: {target: target_name, display: display_name}},
    supervisors: {key: {target: target_name, display: display_name}},
    queues: {key: {target: target_name, display: display_name}},
    contacts: {key: {target: target_name, display: display_name, path: path}},
}
```

Une fois ce JSON rçu par le middleware, celui ci le divise en deux annuaires, un pour le bandeau et un pour le serveur.
Toutes les clefs seront "hashées" afin de garantir l'unicité.
L'exemplaire du bandeau ne contiendra que les clefs hashées et le display name.
L'exemplaire du serveur ne contiendra que les clefs hashées et le target name.

De ce fait le bandeau n'a pas accés aux numéros des contacts.
Lors que le bandeau veut faire un appel vers un élément de l'annuaire il envoie juste un event avec la clef hashée de l'entrée de l'annuaire associée.

La gestion des favoris est externe, elle ne passe pas réellement par l'annuaire mais par un fichier distant stocké sur le serveur du middleware.

Ce fichier distant stocke les favoris, les éléments de configuration du bandeau agent ainsi que l'historique des appels.
Le bandeau demande la lecture de ce fichier au serveur middleware et celui ci lui envoie intégralement. Lors d'une modification le bandeau envoie la totalité du contenu du fichier à écrire.

# Problématiques
## La ressource annuaire n'est pas centralisée
Nous avons les favoris dans un fichier et l'annuaire via une API.
Il serait préférable d'avoir une seule API qui joint les deux sur un simple READ et qui permettrait de mettre à jour les favoris sur un UPDATE.

## Hashage inutile des clés
Il serait préférable que le webadmin fournisse directement des clés préfixés du type ax, sq, qx, cx pour les agents, superviseurs, files et contacts.
Cela permettrait d'économiser un temps de calcul non négligeable sur les gros annuaires.

## Non disponibilité des options de configuration de l'api du webadmin
Actuellement l'api du Webadmin nécéssite un host, un token et un nom de projet.
Ces paramètres ne sont disponible que dans le fichier de configuration du middleware.

## Volume des données qui transite
Lors d'une lecture/écriture sur les favoris (puis historique et configuration du bandeau) l'intégralité du fichier transiste sur le réseau entre le bandeau et le serveur middleware. Cela peut représenter une charge non négligeable et provoquer des saturations chez des clients ayant une faible bande passante.

# Solutions à mettre en place
## Migration de l'utilisation de webadminAPI vers ConfigAPI
Pour se faire, il sera nécessaire de fournir au deploymentAPI, via un script allant chercher le token d'un project dans la BDD du webadmin. Puis de récupérer dans le ConfigAPI ce même token, le nom de l'hote (https://api- + webnode + .interactivmanager.net/) au travers du deploymentAPI.

Il faudra mettre en place un cache:
- soit au niveau du configAPI.
- soit au niveau du deploymentAPI.

## Modification de l'api du webadmin
Au lieu d'envoyer des clés numériques pour chaques entrées de l'annuaire, à ajouter à ces clés un préfixe soulignant leur appartenance à une catégorie. Ce changement permettra de se défaire de la partie hashage des clées coté middleware. 

## Utilisation du configAPI pour loguer un agent
Simple transfert de la partie auth utilisant le webadminAPI du middleware vers le configAPI.
Ce changement permettra de supprimer la partie configuration du webadminAPI du middleware.

## Utilisation du configAPI pour recupérer l'annuaire
Transfert de la partie addressbook utilisant le webadminAPI du middleware vers le configAPI.
Le configAPI devra aussi donner la liste des favoris de l'annuaire si elle existe.
Un check sera nécéssaire afin de savoir si pour un favoris donné, l'entrée existe encore dans le webadmin.

## Utilisation du configAPI pour mettre à jour des favoris
Mettre à jour unitairement un favoris d'un annuaire depuis le bandeau en envoyant un ordre au configAPI depuis le middleware.