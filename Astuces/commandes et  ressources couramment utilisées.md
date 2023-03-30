Cluster

kubectl cluster-info : affiche les informations sur le cluster Kubernetes.
kubectl get nodes : affiche la liste des nœuds du cluster.
kubectl get namespaces : affiche la liste des espaces de noms du cluster.
kubectl describe node/node_name : affiche des informations détaillées sur un nœud spécifique.
Déploiements

kubectl create deployment/deployment_name --image=image_name : crée un nouveau déploiement.
kubectl get deployments : affiche la liste des déploiements.
kubectl rollout status deployment/deployment_name : affiche l'état d'un déploiement.
kubectl rollout undo deployment/deployment_name : annule le déploiement vers une version précédente.
Réplicasets

kubectl get replicasets : affiche la liste des Réplicasets.
kubectl scale deployment/deployment_name --replicas=3 : met à l'échelle un déploiement.
Pods

kubectl get pods : affiche la liste des pods.
kubectl describe pod/pod_name : affiche des informations détaillées sur un pod spécifique.
kubectl delete pod/pod_name : supprime un pod spécifique.
Services

kubectl create service/loadbalancer/service_name --tcp=80:8080 : crée un nouveau service LoadBalancer.
kubectl get services : affiche la liste des services.
kubectl describe service/service_name : affiche des informations détaillées sur un service spécifique.
kubectl delete service/service_name : supprime un service spécifique.
Volumes

kubectl create -f pv.yaml : crée un nouveau volume persistant.
kubectl create -f pvc.yaml : crée une nouvelle réclamation de volume persistant.
kubectl describe pv/pv_name : affiche des informations détaillées sur un volume persistant spécifique.
kubectl describe pvc/pvc_name : affiche des informations détaillées sur une réclamation de volume persistant spécifique.
ConfigMaps et Secrets

kubectl create configmap/configmap_name --from-literal=key=value : crée une nouvelle ConfigMap.
kubectl create secret/generic/secret_name --from-literal=key=value : crée un nouveau secret générique.
kubectl describe configmap/configmap_name : affiche des informations détaillées sur une ConfigMap spécifique.
kubectl describe secret/secret_name : affiche des informations détaillées sur un secret spécifique.