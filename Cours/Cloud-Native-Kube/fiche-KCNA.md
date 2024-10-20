# Cheat Sheet Complet pour la Certification KCNA

## 1. Concepts de Base Kubernetes
- **Kubernetes (K8s)**: Système d'orchestration de conteneurs.
- **Cluster**: Ensemble de nœuds (master et workers).
- **Node**: Machine (virtuelle ou physique) qui exécute des pods.
- **Pod**: Plus petite unité déployable dans Kubernetes, contenant un ou plusieurs conteneurs.
- **Deployment**: Gère des pods et des conteneurs pour assurer la disponibilité.
- **Service**: Expose un ensemble de pods en tant que service réseau unique.

## 2. API Versions
- **Stable**: `v1`
- **Alpha**: `v1alpha1`, `v2alpha1`
- **Beta**: `v1beta1`, `v2beta3`

## 3. Commandes Kubectl Essentielles
- **Vérifier les Pods**: `kubectl get pods`
- **Décrire un Pod**: `kubectl describe pod <pod_name>`
- **Voir les logs d'un Pod**: `kubectl logs <pod_name>`
- **Créer un déploiement**: `kubectl create deployment <name> --image=<image>`
- **Appliquer un fichier de configuration**: `kubectl apply -f <file.yaml>`
- **Supprimer un objet**: `kubectl delete <object_type> <object_name>`
- **Mettre à jour un déploiement**: `kubectl set image deployment/<deployment_name> <container_name>=<new_image>`
- **Voir les services**: `kubectl get services`
- **Voir les namespaces**: `kubectl get namespaces`
- **Changer de contexte**: `kubectl config use-context <context_name>`

## 4. Composants de Kubernetes
### Master Components:
- **etcd**: Stockage de données clé-valeur pour toutes les données de cluster.
- **kube-apiserver**: API Server, point d'entrée pour toutes les commandes.
- **kube-scheduler**: Programme les pods sur les nœuds.
- **kube-controller-manager**: Gère les contrôleurs.
- **cloud-controller-manager**: Intègre Kubernetes aux fournisseurs de cloud.

### Node Components:
- **kubelet**: Agent qui s'exécute sur chaque nœud et gère les pods.
- **kube-proxy**: Gère le réseau sur chaque nœud.
- **Container runtime**: Exécute les conteneurs (Docker, containerd).

## 5. Concepts Avancés
- **StatefulSet**: Pour les applications nécessitant des identifiants réseau persistants.
- **DaemonSet**: Assure qu'un pod tourne sur chaque nœud.
- **ReplicaSet**: Maintient un nombre stable de pods.
- **ConfigMap** et **Secret**: Gérer la configuration et les informations sensibles.
- **Job**: Exécute des tâches spécifiques à exécution unique.
- **CronJob**: Planifie des tâches répétées à intervalles réguliers.

## 6. Observabilité et Surveillance
- **Metrics Server**: Collecte des métriques.
- **Prometheus**: Système de surveillance et d'alerte.
- **Grafana**: Tableau de bord de visualisation.
- **ELK Stack (Elasticsearch, Logstash, Kibana)**: Pour la gestion des logs et la visualisation.
- **Fluentd**: Outil de collecte et de transmission des logs.

### Commandes Prometheus
- **Installation**: Utilisez Helm pour installer Prometheus et Grafana.
  ```sh
  helm install prometheus stable/prometheus
  helm install grafana stable/grafana
  ```
- **AlertManager**: Configurez les alertes pour les conditions spécifiques.

## 7. CI/CD (Intégration Continue / Déploiement Continu)
- **Jenkins**: Serveur d'automatisation open-source.
- **GitLab CI**: Outil CI/CD intégré à GitLab.
- **CircleCI**: Service CI/CD basé sur le cloud.
- **Tekton**: Pipelines CI/CD natifs pour Kubernetes.
- **Argo CD**: Outil de déploiement GitOps pour Kubernetes.

### Concepts Clés CI/CD
- **Pipeline**: Série d'étapes automatisées pour le déploiement.
- **Webhook**: Notification envoyée par un service externe pour déclencher des actions.
- **Artifact**: Fichier produit par le processus de build.

## 8. Networking
- **Service**: Abstraction pour exposer les pods.
  - **ClusterIP**: Expose le service sur une IP interne du cluster.
  - **NodePort**: Expose le service sur le même port sur chaque nœud.
  - **LoadBalancer**: Expose le service en utilisant un load balancer du fournisseur de cloud.
- **Ingress**: Gère l'accès HTTP et HTTPS aux services.
- **Network Policies**: Contrôle le trafic réseau vers et depuis les pods.

### Commandes Ingress
- **Créer un Ingress**: `kubectl apply -f ingress.yaml`
- **Lister les Ingress**: `kubectl get ingress`

## 9. Stockage
- **PersistentVolume (PV)**: Ressource de stockage abstraite.
- **PersistentVolumeClaim (PVC)**: Requête de stockage par les utilisateurs.
- **StorageClass**: Définit les types de stockage.

## 10. Sécurité
- **Namespaces**: Isoler les ressources.
- **RBAC (Role-Based Access Control)**: Contrôler l'accès aux ressources.
- **Network Policies**: Règles de sécurité réseau pour les pods.
- **Pod Security Policies (PSP)**: Gérer la sécurité des pods.

### Commandes RBAC
- **Créer un Role**: `kubectl create role <role_name> --verb=<verb> --resource=<resource>`
- **Créer un RoleBinding**: `kubectl create rolebinding <rolebinding_name> --role=<role_name> --user=<user_name>`

## 11. Concepts de Cloud
- **Cloud Providers**: AWS, GCP, Azure, etc.
- **Managed Kubernetes**: Services Kubernetes gérés comme GKE (Google Kubernetes Engine), EKS (Elastic Kubernetes Service), AKS (Azure Kubernetes Service).
- **Infrastructure as Code (IaC)**: Terraform, Ansible, etc.

## 12. Meilleures Pratiques
- **Namespaces**: Isoler les ressources.
- **RBAC (Role-Based Access Control)**: Contrôler l'accès aux ressources.
- **Resource Quotas**: Gérer les ressources dans les namespaces.
- **Pod Security Policies**: Gérer la sécurité des pods.
- **Labels et Selectors**: Organiser et sélectionner des objets Kubernetes.

### Exemple de Fichier YAML pour Déploiement
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: my-image
        ports:
        - containerPort: 80
```

### Exemple de Fichier YAML pour Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: ClusterIP
```

### Exemple de Fichier YAML pour Ingress
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
spec:
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-service
            port:
              number: 80
```
