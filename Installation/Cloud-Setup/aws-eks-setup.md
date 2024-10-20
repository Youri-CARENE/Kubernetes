# Configuration d'un cluster Kubernetes avec Amazon EKS

## Prérequis
- AWS CLI installée et configurée
- kubectl installé
- eksctl installé

## Étapes de configuration
1. **Créer un cluster EKS** :
   ```bash
   eksctl create cluster --name my-eks-cluster --region us-west-2 --nodegroup-name standard-workers --node-type t2.micro --nodes 3
   ```

2. **Vérifier les nœuds** :
   ```bash
   kubectl get nodes
   ```

## Suppression du cluster
   ```bash
   eksctl delete cluster --name my-eks-cluster
   ```
