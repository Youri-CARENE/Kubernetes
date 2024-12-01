
# Exercice Pratique : Supprimer un Pod Statique dans Kubernetes

## Objectif
Identifier et supprimer un pod statique nommé `static-greenbox`.

---

## Étapes à Suivre

### 1. Identifier le Pod et le Nœud
Utilisez la commande suivante pour localiser le pod et déterminer le nœud où il s'exécute :
```bash
kubectl get pods --all-namespaces -o wide | grep static-greenbox
```
Exemple de sortie :
```plaintext
default       static-greenbox-node01                 1/1     Running   0          19s     10.244.1.2   node01       <none>           <none>
```

Le pod `static-greenbox` s'exécute sur le nœud `node01`.

---

### 2. Accéder au Nœud
Connectez-vous au nœud où le pod s'exécute :
```bash
ssh node01
```

---

### 3. Trouver le Chemin des Pods Statiques
Identifiez le répertoire configuré pour les pods statiques :
1. Recherchez le processus kubelet :
   ```bash
   ps -ef | grep kubelet
   ```
   Exemple de sortie :
   ```plaintext
   /usr/bin/kubelet --config=/var/lib/kubelet/config.yaml
   ```

2. Consultez le fichier `config.yaml` pour trouver le paramètre `staticPodPath` :
   ```bash
   grep -i staticpod /var/lib/kubelet/config.yaml
   ```
   Exemple de sortie :
   ```plaintext
   staticPodPath: /etc/just-to-mess-with-you
   ```

---

### 4. Supprimer le Pod Statique
Accédez au répertoire trouvé dans l'étape précédente et supprimez le fichier YAML du pod :
```bash
cd /etc/just-to-mess-with-you
ls
rm -rf greenbox.yaml
```

---

### 5. Vérifier la Suppression
Retournez au nœud de contrôle (`controlplane`) et confirmez que le pod a été supprimé :
```bash
kubectl get pods --all-namespaces -o wide | grep static-greenbox
```
Si le pod est supprimé avec succès, il n'apparaîtra plus dans la sortie.

---

## Exemple de Fichier YAML pour le Pod Statique

Placez ce fichier dans le répertoire configuré pour les pods statiques (par exemple, `/etc/just-to-mess-with-you/greenbox.yaml`) :

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: static-greenbox
  namespace: default
  labels:
    app: greenbox
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
    readinessProbe:
      httpGet:
        path: /
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 10
    livenessProbe:
      httpGet:
        path: /
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 10
  nodeSelector:
    kubernetes.io/hostname: node01
  tolerations:
  - key: "CriticalAddonsOnly"
    operator: "Exists"
  hostNetwork: false
  dnsPolicy: ClusterFirst
```

---

## Résumé

- **Chemin par Défaut** : `/etc/kubernetes/manifests` (parfois personnalisé).
- **Suppression** : Supprimez simplement le fichier YAML pour arrêter un pod statique.
- **Probes** : Les probes permettent de vérifier l'état du conteneur.

Avec cette procédure, vous pouvez identifier et supprimer tout pod statique configuré dans un cluster Kubernetes.
