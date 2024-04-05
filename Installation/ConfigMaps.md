# ConfigMaps dans Kubernetes

Les ConfigMaps sont des objets Kubernetes qui permettent de stocker des configurations non confidentielles sous forme de paires clé-valeur. Elles peuvent être utilisées pour stocker des configurations fines ou des données utilisées par les pods et les applications Kubernetes.

## Objectifs des ConfigMaps

- **Externaliser les configurations** des applications pour éviter le codage en dur dans les images de conteneurs.
- **Faciliter la modification** des configurations sans nécessiter de reconstruire les images Docker.
- **Partager des configurations** entre différents pods et applications.

## Création d'une ConfigMap

### Via un fichier YAML

Vous pouvez créer une ConfigMap en utilisant un fichier YAML comme suit :

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: ma-configmap
data:
  ma_cle: ma_valeur
  autre_cle: autre_valeur
```

Appliquez le fichier avec `kubectl apply -f ma-configmap.yaml`.

### Via la ligne de commande

Vous pouvez également créer une ConfigMap directement via la ligne de commande :

```bash
kubectl create configmap ma-configmap --from-literal=ma_cle=ma_valeur --from-literal=autre_cle=autre_valeur
```

Ou à partir d'un fichier de propriétés :

```bash
kubectl create configmap ma-configmap --from-file=path/to/my/config.properties
```

## Utilisation d'une ConfigMap

Les ConfigMaps peuvent être utilisées dans vos pods de plusieurs manières :

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
      envFrom:
        - configMapRef:
            name: ma-configmap
```

### En tant que fichier de configuration dans un volume

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
    - name: config-volume
      mountPath: /etc/config
  volumes:
  - name: config-volume
    configMap:
      name: ma-configmap
```

## Bonnes Pratiques

- **Nommez clairement vos ConfigMaps** pour refléter le contenu ou l'usage prévu.
- **Ne stockez pas de données sensibles** dans les ConfigMaps, utilisez des Secrets à la place.
- **Utilisez des ConfigMaps pour des configurations** qui changent fréquemment, cela facilite la mise à jour sans redéploiement.
- **Versionnez vos ConfigMaps** si nécessaire, surtout dans les environnements de production pour un rollback facile.

## Limitations

- Les ConfigMaps ne sont **pas chiffrées** en stockage ou en transit.
- **Taille limitée** : Les ConfigMaps sont stockées dans etcd, qui a une taille maximale de stockage recommandée pour chaque clé/valeur.


