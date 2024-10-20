# Kubernetes (K8s)

Kubernetes, également connu sous le nom de « K8s », est une plate-forme d’orchestration de conteneurs open source permettant d'automatiser le déploiement, la mise à l’échelle et la gestion des applications conteneurisées. Il a été initialement développé par Google et est maintenant maintenu par la Cloud Native Computing Foundation (CNCF).

## Concepts clés

1. **Nœuds** : Machines physiques ou virtuelles exécutant les conteneurs d’application.
2. **Pods** : Plus petites unités déployables dans Kubernetes, contenant un ou plusieurs conteneurs qui partagent les mêmes ressources réseau et de stockage.
3. **Contrôleurs de réplication** : Garantissant qu’un nombre spécifié de répliques d’un espace est en cours d’exécution à tout moment. En cas de défaillance d'un espace, le contrôleur de réplication en crée automatiquement un nouveau pour le remplacer.
4. **Services** : Fournissant une adresse IP stable et un nom DNS pour un ensemble de pods. Ils peuvent également équilibrer la charge du trafic sur plusieurs pods.
5. **Déploiements** : Abstraction de niveau supérieur permettant de gérer le déploiement et la mise à l’échelle des conteneurs d’applications.
6. **ConfigMaps et secrets** : ConfigMaps permettant de gérer les données de configuration séparément du code de l'application, tandis que les secrets permettent de gérer les données sensibles telles que les mots de passe et les clés API.

## Étapes d'utilisation générale

1. **Configurer un cluster Kubernetes** : Configuration d'un cluster de nœuds (serveurs) exécutant les conteneurs d’applications, sur site ou sur une plateforme cloud (Google Cloud, Amazon Web Services (AWS) ou Microsoft Azure). Des outils tels que kubeadm, kops et Kubermatic peuvent aider à cette étape.
2. **Créer et déployer les conteneurs d’application** : Empaquetage du code d’application et de ses dépendances dans des images de conteneur pour les déployer sur le cluster. Docker peut être utilisé pour créer les conteneurs, et l’API de Kubernetes pour créer et gérer des pods. Les abstractions de niveau supérieur de Kubernetes, comme les déploiements et les StatefulSets, peuvent être utilisées pour gérer le déploiement et la mise à l’échelle des conteneurs d’applications.
3. **Gérer l'application** : Une fois les conteneurs en cours d’exécution, ils doivent être gérés à l’aide des outils et des API de Kubernetes. Le tableau de bord Kubernetes peut être utilisé pour afficher et gérer les ressources, ou l’interface de ligne de commande Kubernetes (kubectl) pour gérer les ressources depuis la ligne de commande. Des outils comme Helm peuvent aider à gérer le déploiement et la configuration de l'application.
4. **Surveiller et mettre à l’échelle l'application** : Kubernetes offre des fonctionnalités de surveillance et de mise à l’échelle intégrées permettant d'ajuster automatiquement l'application en fonction de l’utilisation des ressources ou d'autres mesures. Des outils comme Prometheus et Grafana peuvent surveiller les performances et l