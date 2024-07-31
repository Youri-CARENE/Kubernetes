
# Architecture de Base de Kubernetes


## 1. Architecture de Kubernetes

L'architecture de Kubernetes est composée de plusieurs composants répartis entre le **Plan de Contrôle** et les **Nœuds de Travail**.

---

### A. Plan de Contrôle

Le Plan de Contrôle gère l'ensemble du cluster Kubernetes. Il est responsable de prendre des décisions globales concernant le cluster et de détecter et répondre aux événements du cluster.

1. **Serveur API (kube-apiserver)**
   - **Rôle** : Expose l'API de Kubernetes.
   - **Fonction** : Point de communication central pour tous les composants Kubernetes et interface principale pour l'administration du cluster.

2. **Etcd**
   - **Rôle** : Stockage des données de configuration.
   - **Fonction** : Base de données clé-valeur distribuée qui stocke toutes les informations d'état du cluster.

3. **Planificateur (kube-scheduler)**
   - **Rôle** : Planification des pods sur les nœuds.
   - **Fonction** : Planifie les pods non assignés sur les nœuds en fonction des ressources disponibles et des contraintes définies.

4. **Gestionnaire de Contrôleur (kube-controller-manager)**
   - **Rôle** : Exécution des contrôleurs.
   - **Fonction** : Gère divers contrôleurs comme ReplicaSet, Deployment, DaemonSet, en assurant que l'état réel du cluster correspond à l'état désiré.

---

### B. Nœuds de Travail

Les Nœuds de Travail exécutent les applications conteneurisées. Chaque nœud dispose des services nécessaires pour exécuter des pods et est géré par le Plan de Contrôle.

1. **Kubelet**
   - **Rôle** : Agent du nœud.
   - **Fonction** : Assure que les conteneurs sont exécutés dans les pods, interagit avec le plan de contrôle pour obtenir les informations nécessaires et contrôle l'état des pods.

2. **Kube-proxy**
   - **Rôle** : Gestion du réseau du cluster.
   - **Fonction** : Maintient les règles de réseau sur les nœuds, permettant la communication réseau des pods et l'équilibrage de la charge du trafic réseau.

3. **Runtime de Conteneur**
   - **Rôle** : Exécution des conteneurs.
   - **Fonction** : Exécute et gère le cycle de vie des conteneurs (comme Docker, containerd).

---

### C. Diagramme de l'Architecture de Kubernetes

```plaintext
+------------------------------------+
|           Plan de Contrôle         |
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
|           Nœuds de Travail         |
+------------------------------------+
|                                    |
|  +-----------------------------+   |
|  |           Kubelet           |   |
|  +-----------------------------+   |
|  |          Kube-proxy         |   |
|  +-----------------------------+   |
|  |     Runtime de Conteneur    |   |
|  +-----------------------------+   |
|                                    |
|  +-----------------------------+   |
|  |           PODS              |   |
|  |  +----------------------+   |   |
|  |  |  Conteneurs          |   |   |
|  |  +----------------------+   |   |
|  +-----------------------------+   |
|                                    |
+------------------------------------+
```

---

## 2. Flux de Travail Général

- **Déploiement d'Application** : Les utilisateurs définissent des applications dans des fichiers de configuration YAML. Ces fichiers sont envoyés au Serveur API.
- **Planification et Allocation** : Le Planificateur assigne des pods aux nœuds disponibles.
- **Exécution** : Le Kubelet sur chaque nœud exécute les conteneurs définis dans les pods.
- **Réseautage et Services** : Kube-proxy gère la communication réseau entre les pods et le monde extérieur.

---

### Conclusion

Kubernetes offre une orchestration de conteneurs flexible et puissante, garantissant une haute disponibilité, une mise à l'échelle automatique et une gestion simplifiée des applications conteneurisées.
