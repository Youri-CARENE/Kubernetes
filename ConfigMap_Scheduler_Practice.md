
# Exercice Pratique : ConfigMap et Scheduler dans Kubernetes

## Objectif
Créer un `ConfigMap` pour un nouveau scheduler et l'utiliser comme volume dans un pod Kubernetes.

---

## Contexte
- Un fichier de définition de ConfigMap est déjà fourni : `/root/my-scheduler-configmap.yaml`.
- Ce fichier crée un `ConfigMap` nommé **my-scheduler-config** à partir du contenu d’un fichier existant : `/root/my-scheduler-config.yaml`.

---

## Étapes à Suivre

### 1. Vérifier le Contenu du Fichier `my-scheduler-configmap.yaml`

Avant de créer le `ConfigMap`, inspectez le fichier YAML pour comprendre sa structure :
```bash
cat /root/my-scheduler-configmap.yaml
```
Exemple de contenu :
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-scheduler-config
  namespace: kube-system
data:
  scheduler-config.json: |
    {
      "apiVersion": "kubescheduler.config.k8s.io/v1beta1",
      "kind": "KubeSchedulerConfiguration",
      "clientConnection": {
        "kubeconfig": "/etc/kubernetes/scheduler.conf"
      },
      "leaderElection": {
        "leaderElect": true
      }
    }
```

Ce fichier utilise un fichier source `/root/my-scheduler-config.yaml` pour inclure les données dans le `ConfigMap`.

---

### 2. Créer le ConfigMap
Appliquez le fichier pour créer le `ConfigMap` :
```bash
kubectl apply -f /root/my-scheduler-configmap.yaml
```

### 3. Vérifier la Création du ConfigMap
Assurez-vous que le `ConfigMap` a été créé avec succès :
```bash
kubectl get configmap -n kube-system | grep my-scheduler-config
```
Pour afficher les détails :
```bash
kubectl describe configmap my-scheduler-config -n kube-system
```

---

### 4. Utiliser le ConfigMap comme Volume

Pour utiliser ce `ConfigMap` dans un pod, ajoutez-le comme volume dans le fichier YAML du pod. Exemple :
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: custom-scheduler
  namespace: kube-system
spec:
  containers:
  - name: scheduler
    image: k8s.gcr.io/kube-scheduler:v1.27.3
    volumeMounts:
    - name: scheduler-config-volume
      mountPath: /etc/kubernetes/scheduler-config
  volumes:
  - name: scheduler-config-volume
    configMap:
      name: my-scheduler-config
```

---

### 5. Déployer et Vérifier
1. Appliquez le fichier YAML du pod :
   ```bash
   kubectl apply -f custom-scheduler.yaml
   ```

2. Vérifiez que le pod utilise bien le `ConfigMap` comme volume :
   ```bash
   kubectl describe pod custom-scheduler -n kube-system
   ```

---

## Points Clés
1. **ConfigMap comme Volume** :
   - Permet de monter des configurations directement dans les pods sans les inclure dans l’image Docker.

2. **Namespace Important** :
   - Le namespace du `ConfigMap` et du pod doit correspondre (dans cet exemple, `kube-system`).

3. **Commandes Essentielles** :
   - `kubectl apply -f <file>` pour créer des objets Kubernetes.
   - `kubectl describe configmap <name>` pour afficher les détails d’un `ConfigMap`.

---

## Résumé
Avec ce cas pratique, vous avez appris à :
- Créer un `ConfigMap` à partir d’un fichier.
- Utiliser un `ConfigMap` comme volume dans un pod.
- Vérifier l’application et la configuration dans un environnement Kubernetes.

