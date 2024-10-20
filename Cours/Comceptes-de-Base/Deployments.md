# Deployments dans Kubernetes

Les `Deployments` dans Kubernetes permettent de décrire un état désiré pour vos applications, notamment en termes de pods et de réplicas, gérant ainsi le déploiement et la mise à jour des applications de manière déclarative.

## Objectif des Deployments

Les Deployments visent à faciliter :

- **Le déploiement d'applications sans état et avec état**
- **La mise à jour déclarative des applications**
- **Le rollback (retour à une version antérieure) d'applications**
- **La mise à l'échelle des applications**
- **La gestion de l'état désiré de l'application**

## Définition d'un Deployment

Un Deployment est défini via un fichier YAML. Voici un exemple :

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mon-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: mon-application
  template:
    metadata:
      labels:
        app: mon-application
    spec:
      containers:
      - name: mon-container
        image: mon-image:1.0.0
        ports:
        - containerPort: 80
```

Dans cet exemple, le Deployment crée trois réplicas du pod, chacun basé sur l'image `mon-image:1.0.0`.

## Commandes Utiles

### Créer un Deployment

```bash
kubectl apply -f mon-deployment.yaml
```

### Obtenir l'état des Deployments

```bash
kubectl get deployments
```

### Mettre à jour un Deployment

Modifier d'abord le fichier YAML, puis appliquer les changements :

```bash
kubectl apply -f mon-deployment.yaml
```

### Mise à l'échelle d'un Deployment

```bash
kubectl scale deployment mon-deployment --replicas=5
```

### Rollback d'un Deployment

```bash
kubectl rollout undo deployment mon-deployment
```

## Fonctionnement

Un Deployment crée un ou plusieurs ReplicaSets pour assurer la gestion des pods. Chaque mise à jour crée un nouveau ReplicaSet, permettant des rollbacks faciles.

## Différences Clés

- **Pods** : Plus petite unité déployable. Un pod représente un processus en cours d'exécution dans votre cluster.
- **Deployments** : Gèrent les ReplicaSets pour déployer des applications stateless. Idéal pour la gestion de version et la mise à l'échelle.
- **Services** : Abstraction qui définit un ensemble logique de Pods et une politique d'accès à ces pods, souvent via un IP fixe ou un nom DNS.
