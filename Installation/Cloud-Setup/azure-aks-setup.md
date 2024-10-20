# Configuration d'un cluster Kubernetes avec Azure AKS

## Prérequis
- Azure CLI installée
- Compte Azure avec les permissions nécessaires

## Étapes de configuration
1. **Connecter votre compte Azure** :
   ```bash
   az login
   ```

2. **Créer un groupe de ressources** :
   ```bash
   az group create --name myResourceGroup --location eastus
   ```

3. **Créer un cluster AKS** :
   ```bash
   az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 3 --enable-addons monitoring --generate-ssh-keys
   ```

4. **Se connecter au cluster** :
   ```bash
   az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
   ```

## Suppression du cluster
   ```bash
   az aks delete --resource-group myResourceGroup --name myAKSCluster
   ```
