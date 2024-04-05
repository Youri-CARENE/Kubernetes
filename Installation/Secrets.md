# Secrets dans Kubernetes

Les Secrets permettent de stocker et de gérer des informations sensibles, telles que des mots de passe, des jetons OAuth, et des clés ssh, de manière sécurisée.

## Objectifs des Secrets

- **Protéger les informations sensibles** : Éviter le stockage des données sensibles dans le code source ou les images Docker.
- **Centraliser la gestion des secrets** : Gérer les secrets de manière centralisée et les injecter dans les pods au besoin.

## Création d'un Secret

### Via un fichier YAML

Vous pouvez créer un Secret en utilisant un fichier YAML. Les valeurs doivent être encodées en base64.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mon-secret
type: Opaque
data:
  username: dXNlcm5hbWU= # "username" encodé en base64
  password: cGFzc3dvcmQ= # "password" encodé en base64
```

Appliquez le fichier avec `kubectl apply -f mon-secret.yaml`.

### Via la ligne de commande

Créez un Secret directement avec kubectl sans avoir besoin de l'encoder en base64 :

```bash
kubectl create secret generic mon-secret --from-literal=username=user --from-literal=password=pass
```

## Utilisation d'un Secret

Les Secrets peuvent être utilisés dans vos pods de plusieurs façons :

### En tant que variables d'environnement

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mon-pod
spec:
  containers:
  - name: mon-conteneur
    image: mon-image
    env:
      - name: USERNAME
        valueFrom:
          secretKeyRef:
            name: mon-secret
            key: username
      - name: PASSWORD
        valueFrom:
          secretKeyRef:
            name: mon-secret
            key: password
```

### En tant que fichier dans un volume

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mon-pod
spec:
  containers:
  - name: mon-conteneur
    image: mon-image
    volumeMounts:
    - name: secret-volume
      mountPath: "/etc/secret"
      readOnly: true
  volumes:
  - name: secret-volume
    secret:
      secretName: mon-secret
```

## Bonnes Pratiques

- **Limitez l'accès** : Utilisez les contrôles d'accès RBAC pour limiter qui peut lire et écrire les Secrets.
- **Ne stockez pas de Secrets dans vos images Docker** : Injectez les Secrets au moment de l'exécution plutôt que de les construire dans l'image.
- **Rotation régulière des Secrets** : Mettez régulièrement à jour et remplacez vos Secrets pour améliorer la sécurité.

## Cas d'Usage

- Stocker des informations d'authentification pour accéder à une base de données.
- Contenir des clés privées SSL/TLS pour des communications sécurisées.
- Garder des jetons d'accès pour des services externes comme AWS, Google Cloud, ou des APIs.

## Commandes Utiles

- **Créer un Secret** : `kubectl create secret`
- **Lister tous les Secrets** : `kubectl get secrets`
- **Voir le détail d'un Secret** : `kubectl describe secret mon-secret`
- **Mettre à jour un Secret** : Modifiez le fichier YAML et appliquez-le avec `kubectl apply`, ou utilisez `kubectl edit secret mon-secret` pour une édition interactive.

