# Namespaces dans Kubernetes

Les namespaces Kubernetes fournissent une isolation logique des ressources au sein d'un cluster. Ils permettent de diviser les ressources du cluster entre plusieurs utilisateurs et projets, facilitant ainsi la gestion des accès, la segmentation et l'allocation des ressources.

## Objectif des Namespaces

Les namespaces sont essentiels pour :

- **Isoler les ressources** : Séparer les ressources par équipe, application, environnement de développement/test/production.
- **Contrôler l'accès** : Restreindre l'accès aux ressources du cluster en fonction des namespaces.
- **Optimiser l'utilisation des ressources** : Attribuer des quotas de ressources pour gérer l'utilisation du cluster efficacement.

## Namespaces par Défaut

Kubernetes comprend plusieurs namespaces par défaut :

- **`default`** : Pour les objets sans namespace spécifié.
- **`kube-system`** : Pour les objets créés par le système Kubernetes lui-même.
- **`kube-public`** : Un espace pour les ressources visibles à travers tout le cluster.
- **`kube-node-lease`** : Contient les informations de lease des nœuds pour améliorer la performance et l'efficacité du heartbeating des nœuds.

## Définition d'un Namespace

Pour définir un namespace, utilisez un fichier YAML comme suit :

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: mon-namespace
```

## Commandes Utiles

### Création et Gestion

- **Créer un namespace** : `kubectl create namespace mon-namespace`
- **Appliquer un fichier YAML** : `kubectl apply -f mon-namespace.yaml`

### Visualisation et Sélection

- **Lister tous les namespaces** : `kubectl get namespaces`
- **Définir le namespace par défaut pour kubectl** : `kubectl config set-context --current --namespace=mon-namespace`
- **Voir les ressources dans un namespace spécifique** : `kubectl get pods --namespace=mon-namespace`

### Suppression

- **Supprimer un namespace** : `kubectl delete namespaces mon-namespace`

## Astuces

- **Séparation des Environnements** : Utilisez différents namespaces pour séparer clairement les environnements de développement, de test, et de production.
- **Quotas** : Configurez des quotas de ressources pour les namespaces pour éviter le surprovisionnement des ressources par une équipe ou une application.
- **Politiques de Sécurité** : Appliquez des politiques de sécurité spécifiques à chaque namespace pour améliorer la sécurité au niveau du cluster.

## Autres Informations Utiles

- **Roles et Permissions** : Les namespaces jouent un rôle clé dans la définition des rôles et permissions via les RoleBindings et ClusterRoleBindings, permettant une gestion fine des accès aux ressources.
- **Réseau** : Les politiques de réseau peuvent être appliquées au niveau des namespaces pour contrôler la communication entre les pods de différents namespaces.
- **Stockage** : Certains types de volumes, comme `ConfigMap` ou `Secret`, peuvent être limités à un namespace, renforçant l'isolation et la sécurité des données.
