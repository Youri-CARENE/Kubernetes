# Installation de Kubernetes avec kind
kind (Kubernetes IN Docker) permet de créer des clusters Kubernetes dans Docker.

## Prérequis
- Docker installé
- Go installé (optionnel)

## Étapes d'installation
1. **Installer kind** :
   ```bash
   go install sigs.k8s.io/kind@latest
   ```

2. **Créer un cluster Kubernetes** :
   ```bash
   kind create cluster --name my-cluster
   ```

3. **Vérifier l'installation** :
   ```bash
   kubectl cluster-info --context kind-my-cluster
   ```

## Suppression du cluster
Pour supprimer le cluster créé :
   ```bash
   kind delete cluster --name my-cluster
   ```
