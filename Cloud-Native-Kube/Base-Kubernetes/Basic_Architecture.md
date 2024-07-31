# Architecture de Base de Kubernetes


## . Architecture de Kubernetes

L'architecture de Kubernetes est composée de plusieurs composants répartis entre le **Control Plane** et les **Worker Nodes**.

---

### A. Control Plane

Le Control Plane gère l'ensemble du cluster Kubernetes. Il est responsable de prendre des décisions globales concernant le cluster et de détecter et répondre aux événements du cluster.

1. **API Server (kube-apiserver)**
   - **Rôle** : Expose l'API de Kubernetes.
   - **Fonction** : Point de communication central pour tous les composants Kubernetes et interface principale pour l'administration du cluster.

2. **Etcd**
   - **Rôle** : Stockage des données de configuration.
   - **Fonction** : Base de données clé-valeur distribuée qui stocke toutes les informations d'état du cluster.

3. **Scheduler (kube-scheduler)**
   - **Rôle** : Planification des pods sur les nœuds.
   - **Fonction** : Planifie les pods non assignés sur les nœuds en fonction des ressources disponibles et des contraintes définies.

4. **Controller Manager (kube-controller-manager)**
   - **Rôle** : Exécution des contrôleurs.
   - **Fonction** : Gère divers contrôleurs comme ReplicaSet, Deployment, DaemonSet, en assurant que l'état réel du cluster correspond à l'état désiré.

---

### B. Worker Nodes

Les Worker Nodes exécutent les applications conteneurisées. Chaque nœud dispose des services nécessaires pour exécuter des pods et est géré par le Control Plane.

1. **Kubelet**
   - **Rôle** : Agent du nœud.
   - **Fonction** : Assure que les conteneurs sont exécutés dans les pods, interagit avec le Control Plane pour obtenir les informations nécessaires et contrôle l'état des pods.

2. **Kube-proxy**
   - **Rôle** : Gestion du réseau du cluster.
   - **Fonction** : Maintient les règles de réseau sur les nœuds, permettant la communication réseau des pods et l'équilibrage de la charge du trafic réseau.

3. **Container Runtime**
   - **Rôle** : Exécution des conteneurs.
   - **Fonction** : Exécute et gère le cycle de vie des conteneurs (comme Docker, containerd).

---

### C. Diagramme de l'Architecture de Kubernetes

```plaintext
+------------------------------------+
|           Control Plane            |
+------------------------------------+
|                                    |
|  +-----------------------------+   |
|  |        kube-apiserver       |   |
|  +-----------------------------+   |
|  |            etcd             |   |
|  +-----------------------------+   |
|  |      kube-scheduler         |   |
|  +-----------------------------+   |
|  |  kube-controller-manager    |   |
|  +-----------------------------+   |
|                                    |
+------------------------------------+
                |
                |
                v
+------------------------------------+
|           Worker Nodes             |
+------------------------------------+
|                                    |
|  +-----------------------------+   |
|  |           Kubelet           |   |
|  +-----------------------------+   |
|  |          Kube-proxy         |   |
|  +-----------------------------+   |
|  |     Container Runtime       |   |
|  +-----------------------------+   |
|                                    |
|  +-----------------------------+   |
|  |           PODS              |   |
|  |  +----------------------+   |   |
|  |  |  Containers          |   |   |
|  |  +----------------------+   |   |
|  +-----------------------------+   |
|                                    |
+------------------------------------+
```

---

## . Flux de Travail Général

- **Déploiement d'Application** : Les utilisateurs définissent des applications dans des fichiers de configuration YAML. Ces fichiers sont envoyés au API Server.
- **Planification et Allocation** : Le Scheduler assigne des pods aux nœuds disponibles.
- **Exécution** : Le Kubelet sur chaque nœud exécute les conteneurs définis dans les pods.
- **Réseautage et Services** : Kube-proxy gère la communication réseau entre les pods et le monde extérieur.

---

### Conclusion

Kubernetes offre une orchestration de conteneurs flexible et puissante, garantissant une haute disponibilité, une mise à l'échelle automatique et une gestion simplifiée des applications conteneurisées.
