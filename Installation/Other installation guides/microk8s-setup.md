# Installation de MicroK8s

## Prérequis
- Système Ubuntu ou dérivé

## Étapes d'installation
1. **Installer MicroK8s** :
   ```bash
   sudo snap install microk8s --classic
   ```

2. **Ajouter votre utilisateur au groupe MicroK8s** :
   ```bash
   sudo usermod -aG microk8s $USER
   newgrp microk8s
   ```

3. **Vérifier l'installation** :
   ```bash
   microk8s status --wait-ready
   microk8s kubectl get nodes
   ```

## Commandes utiles
   ```bash
   # Activer des add-ons
   microk8s enable dns dashboard
   ```
