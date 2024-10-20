# Activer Kubernetes sur Docker Desktop
Docker Desktop offre une option intégrée pour activer Kubernetes.

## Prérequis
- Docker Desktop installé (Windows ou Mac)

## Étapes d'activation
1. **Ouvrir Docker Desktop**.
2. **Accéder aux Paramètres** > **Kubernetes**.
3. **Cocher "Enable Kubernetes"** et cliquer sur "Apply & Restart".

## Vérification
Une fois Docker Desktop redémarré, vérifiez le statut de Kubernetes :
   ```bash
   kubectl config view
   kubectl get nodes
   ```

## Désactivation
Pour désactiver Kubernetes, décochez simplement "Enable Kubernetes" et redémarrez Docker Desktop.
