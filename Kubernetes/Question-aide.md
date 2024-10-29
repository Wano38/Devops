# Kubernetes Aide / Question / Commande

## Exercice 1 :

1. En utilisant la cheatsheet k8s, créer un fichier décrivant un Pod utilisant une image nginx pour créer un pod nommé web.

   ```yaml
   apiVersion: v1 # Version de l'APIServer k8s
   kind: Pod # Le type de ressource à gérer : Pod, Deployment, Service, ...
   metadata: # Métadatas de la ressource
     name: kuber1 # nom (interne) de la ressource à créer et/ou monitorer
   spec: # Les spécifications de la ressource. Différent pour chaque type de ressource
     containers:
     - name: front-end # nom du conteneur
       image: nginx # image Docker
       ports:
       - containerPort: 80 # port dans le conteneur
       ```
2. Récupérer l’adresse IP du pod créé.

```bash
kubectl get pods -o wide
```

3. Créer un 2e pod nommé test et utilisant une image alpine. On exécutera une commande sleep 9999 pour faire tourner ce pod en continue.

```yaml

apiVersion: v1  # Version de l'APIServer k8s
kind: Pod  # Le type de ressource à gérer : Pod, Deployment, Service, ...
metadata:  # Métadatas de la ressource
  name: test  # nom (interne) de la ressource à créer et/ou monitorer
spec:  # Les spécifications de la ressource. Différent pour chaque type de ressource
  containers:
    - name: front-end  # nom du conteneur
      image: alpine  # image Docker
      command:  # Commande à exécuter dans le conteneur
        - sleep
        - "9999"
      ports:  # Définition des ports exposés par le conteneur
        - containerPort: 80  # port dans le contene
        
```
4. Se connecter au pod test et exécuter un ping du pod web.

5. Détruire le conteneur de test.

6. Lancer mon pod :
```bash
kubectl apply -f monFichier.yml
```

## Exercice 2 :

1. En utilisant la ligne de commande kubectl, exposer un port du pod nginx
   ```bash
   kubectl port-forward web 8080:80 & 
   
   ```
2. Modifier le pod web pour lui ajouter un label : app=web-app. Ce label permettre de
lier le Pod aux Services.
```bash
kubectl label pods web app=web-app
```
3. Créer un service de type ClusterIP pour exposer nginx dans le cluster. Tester la
connexion depuis un 2e Pod.
```yaml
apiVersion: v1 # Version de l'APIServer k8s
kind: Service # Le type de ressource à gérer : Pod, Deployment, Service, ...
metadata: # Métadatas de la ressource
  name: my-clusterip-service # nom (interne) de la ressource à créer et/ou monitorer
  labels: # Correction : ajout d'un espace
    app: web-app
spec:
  type: ClusterIP
  selector:
    app: web-app
  ports:
    - port: 8080 # Port interne exposé par le service
      targetPort: 80 # Port interne sur lequel le conteneur écoute
```

4. Créer un service de type NodePort. Tester l’accès à nginx depuis la machine hôte
sur le port choisi.



## Exercice 3 :
1. Ajouter un nouveau label à l’un des WorkerNode.
   
2. Créer un pod avec une affinité pour ce WorkerNode.
   
3. Vérifier que le Pod a été démarré sur le bon Node.

## Exercice 4 :
1. Ajouter un label app=web-app au Pod web et vérifier l’ajout.
   
2. Créer un Pod cache tournant un conteneur redis avec une affinité pour le Pod web.
Vérifier l’affinité.

3. Créer un Pod antagoniste tournant un conteneur alpine avec une anti-affinité
pour le Pod web. Vérifier la non-affinité.