## Synthèse et Explication Concise sur Divers Concepts de Kubernetes

---

#### 1. Manual Scheduling

**Manual Scheduling** est le processus par lequel un administrateur Kubernetes spécifie manuellement sur quel nœud un pod doit être exécuté. Cela se fait en définissant explicitement le champ `nodeName` dans la spécification du pod.

**Exemple** :
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: manual-scheduled-pod
spec:
  containers:
  - name: nginx
    image: nginx
  nodeName: node01
```

---

#### 2. Labels and Selectors

**Labels** sont des paires clé-valeur attachées aux objets Kubernetes, utilisés pour organiser et sélectionner des sous-ensembles d'objets.

**Selectors** permettent de sélectionner des objets en fonction de leurs labels.

**Exemple de Label** :
```yaml
metadata:
  labels:
    app: frontend
    env: production
```

**Exemple de Selectors** :
```yaml
selector:
  matchLabels:
    app: frontend
    env: production
```

---

#### 3. Taints and Tolerations

**Taints** sont appliqués aux nœuds pour empêcher certains pods d'y être planifiés.

**Tolerations** permettent aux pods d'être planifiés sur des nœuds avec des taints correspondants.

**Exemple de Taint** :
```
kubectl taint nodes node1 key=value:NoSchedule
```

**Exemple de Toleration** :
```yaml
tolerations:
- key: "key"
  operator: "Equal"
  value: "value"
  effect: "NoSchedule"
```

---

#### 4. Node Selectors

**Node Selectors** sont des sélecteurs simples pour contraindre les pods à s'exécuter sur des nœuds spécifiques en utilisant des labels.

**Exemple** :
```yaml
spec:
  nodeSelector:
    disktype: ssd
```

---

#### 5. Node Affinity

**Node Affinity** est une version avancée de `nodeSelector` qui permet des règles plus expressives pour la planification des pods.

**Exemple** :
```yaml
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
      - matchExpressions:
        - key: disktype
          operator: In
          values:
          - ssd
```

---

#### 6. Taints and Tolerations vs Node Affinity

- **Taints and Tolerations** : Utilisés pour empêcher certains pods d'être planifiés sur certains nœuds sauf s'ils tolèrent les taints.
- **Node Affinity** : Utilisé pour préférer ou requérir la planification des pods sur certains nœuds basés sur les labels des nœuds.

---

#### 7. Resource Limits

**Resource Limits** définissent les ressources (CPU, mémoire) qu'un conteneur peut utiliser.

**Exemple** :
```yaml
resources:
  limits:
    memory: "128Mi"
    cpu: "500m"
  requests:
    memory: "64Mi"
    cpu: "250m"
```

---

#### 8. DaemonSets

**DaemonSets** assurent que tous (ou certains) nœuds exécutent une copie d'un pod.

**Exemple** :
```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: node-exporter
spec:
  selector:
    matchLabels:
      name: node-exporter
  template:
    metadata:
      labels:
        name: node-exporter
    spec:
      containers:
      - name: node-exporter
        image: prom/node-exporter
```

---

#### 9. Static Pods

**Static Pods** sont gérés directement par le kubelet sur un nœud spécifique et ne sont pas contrôlés par le plan de contrôle.

**Exemple** :
Définir un pod statique dans `/etc/kubernetes/manifests/` :
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: static-pod
spec:
  containers:
  - name: nginx
    image: nginx
```

---

#### 10. Multiple Schedulers

**Multiple Schedulers** permet d'exécuter plusieurs planificateurs dans un cluster, chacun avec une politique de planification différente.

**Exemple** :
Déployer un planificateur personnalisé :
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: custom-scheduler
spec:
  containers:
  - name: scheduler
    image: my-custom-scheduler
```

---

#### 11. Configuring Kubernetes Scheduler Profiles

**Scheduler Profiles** permettent de définir différentes stratégies de planification dans un seul planificateur.

**Exemple** :
Configurer un profil de planification :
```yaml
apiVersion: kubescheduler.config.k8s.io/v1beta1
kind: KubeSchedulerConfiguration
profiles:
- schedulerName: my-scheduler
  plugins:
    queueSort:
      enabled:
        - name: PrioritySort
```