# Documentation sur l'utilisation de Docker®

Ce document présente des informations sur l'exposition des logs des applications à Docker®, la récupération dynamique des logs, la limitation des ressources d'un conteneur et les bonnes pratiques associées.

## 1. Exposition des logs par les applications

Les applications exposent les logs à Docker® de plusieurs manières. Nous privilégions l'utilisation d'une application qui affiche les statistiques des conteneurs, leurs fichiers d'environnement, les statistiques et les logs. Cela permet d'avoir une vue d'ensemble des performances et de l'état des conteneurs.

## 2. Récupération dynamique des logs des conteneurs

Pour récupérer dynamiquement les logs des conteneurs en cours d'exécution, vous pouvez utiliser la commande suivante :

```bash
docker logs -f lazydocker