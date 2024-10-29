#  Kubernetes Aide / Question / Commande

## Comment faire un PODS : 

   ```bash
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

## Lancer mon pod :
```bash
kubectl apply -f monFichier.yml
 ```
