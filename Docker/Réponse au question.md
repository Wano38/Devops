# Documentation sur l'utilisation de Docker®

Ce document présente des informations sur l'exposition des logs des applications à Docker®, la récupération dynamique des logs, la limitation des ressources d'un conteneur et les bonnes pratiques associées.

## 1. Exposition des logs par les applications

Les applications peuvent exposer les logs à Docker® de plusieurs manières. Nous privilégions l'utilisation d'une application qui affiche :

- Les statistiques des conteneurs
- Leurs fichiers d'environnement
- Les statistiques et les logs

Cette approche permet d'avoir une vue d'ensemble des performances et de l'état des conteneurs.

## 2. Récupération dynamique des logs des conteneurs

Pour récupérer dynamiquement les logs des conteneurs en cours d'exécution, vous pouvez utiliser la commande suivante :

```bash
docker logs -f lazydocker
```

## 3. Limitation des ressources d'un conteneur

Pour limiter les ressources disponibles pour un conteneur, utilisez la commande suivante :

```bash
docker run -it -d --name mon_conteneur3 --memory="512m" --cpus="1.5" bash
```

### 3.1 Changement des ressources d’un conteneur en cours d’exécution

Changer les ressources d’un conteneur en cours d’exécution est généralement limité dans Docker. Voici quelques bonnes pratiques à suivre :

1. **Redémarrage du conteneur** : La méthode la plus courante pour modifier les ressources consiste à arrêter le conteneur, puis à le supprimer et à le redémarrer avec les nouvelles ressources. Utilisez les commandes suivantes :

   ```bash
   docker stop <container_id>
   docker rm <container_id>
   docker run --name <nom_du_conteneur> --memory="1g" --cpus="2" <image>
   ```

## 4. Bonnes pratiques

- **Surveillance des ressources** : Utilisez des outils comme `docker stats` pour surveiller l'utilisation des ressources des conteneurs.
- **Utilisation d'outils de logging** : Considérez l'utilisation de solutions de gestion des logs comme ELK stack (Elasticsearch, Logstash, Kibana) ou Grafana pour une visualisation et une gestion avancées des logs.
- **Éviter les limites trop strictes** : Évitez de définir des limites trop strictes sur les ressources, car cela peut affecter les performances des applications.
