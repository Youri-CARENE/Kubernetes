# Commandes Kubernetes

## Cluster

- `kubectl cluster-info` : Afficher les informations sur le cluster Kubernetes.
- `kubectl get nodes` : Afficher la liste des nœuds du cluster.
- `kubectl get namespaces` : Afficher la liste des espaces de noms du cluster.
- `kubectl describe node/<node_name>` : Afficher des informations détaillées sur un nœud spécifique.

## Déploiements

- `kubectl create deployment/<deployment_name> --image=<image_name>` : Créer un nouveau déploiement.
- `kubectl get deployments` : Afficher la liste des déploiements.
- `kubectl rollout status deployment/<deployment_name>` : Afficher l'état d'un déploiement.
- `kubectl rollout undo deployment/<deployment_name>` : Annuler le déploiement vers une version précédente.

## Réplicasets

- `kubectl get replicasets` : Afficher la liste des Réplicasets.
- `kubectl scale deployment/<deployment_name> --replicas=3` : Mettre à l'échelle un déploiement.

## Pods

- `kubectl get pods` : Afficher la liste des pods.
- `kubectl describe pod/<pod_name>` : Afficher des informations détaillées sur un pod spécifique.
- `kubectl delete pod/<pod_name>` : Supprimer un pod spécifique.

## Services

- `kubectl create service/loadbalancer/<service_name> --tcp=80:8080` : Créer un nouveau service LoadBalancer.
- `kubectl get services` : Afficher la liste des services.
- `kubectl describe service/<service_name>` : Afficher des informations détaillées sur un service spécifique.
- `kubectl delete service/<service_name>` : Supprimer un service spécifique.

## Volumes

- `kubectl create -f pv.yaml` : Créer un nouveau volume persistant.
- `kubectl create -f pvc.yaml` : Créer une nouvelle réclamation de volume persistant.
- `kubectl describe pv/<pv_name>` : Afficher des informations détaillées sur un volume persistant spécifique.
- `kubectl describe pvc/<pvc_name>` : Afficher des informations détaillées sur une réclamation de volume persistant spécifique.

## ConfigMaps et Secrets

- `kubectl create configmap/<configmap_name> --from-literal=key=value` : Créer une nouvelle ConfigMap.
- `kubectl create secret/generic/<secret_name> --from-literal=key=value` : Créer un nouveau secret générique.
- `kubectl describe configmap/<configmap_name>` : Afficher des informations détaillées sur une ConfigMap spécifique.
- `kubectl describe secret/<secret_name>` : Afficher des informations détaillées sur un secret spécifique.