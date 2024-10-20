# Installation de k3s avec Docker
k3s est une version allégée de Kubernetes qui peut fonctionner sur un seul nœud ou être configurée en cluster.

## Prérequis
- Docker installé (version recommandée : 20.x ou plus)
- Connexion Internet active

## Étapes d'installation
1. **Installer k3s** :
   ```bash
   curl -sfL https://get.k3s.io | sh -
   ```

2. **Vérifier l'état du cluster** :
   ```bash
   kubectl get nodes
   ```

## Configuration
Vous pouvez configurer k3s pour utiliser Docker comme moteur de conteneurs par défaut :
   ```bash
   curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC="--docker" sh -
   ```
