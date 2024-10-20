# Installation de k3s : Version allégée de Kubernetes

## Prérequis
- Système Linux avec Docker installé
- Connexion Internet

## Étapes d'installation
1. **Télécharger et installer k3s** :
   ```bash
   curl -sfL https://get.k3s.io | sh -
   ```

2. **Vérifier l'installation** :
   ```bash
   kubectl get nodes
   ```

## Commandes utiles
   ```bash
   # Redémarrer k3s
   systemctl restart k3s
   ```
