# Configuration d'un cluster Kubernetes avec Google GKE

## Prérequis
- Google Cloud SDK installé
- Compte de facturation Google Cloud actif

## Étapes de configuration
1. **Authentifier votre compte Google Cloud** :
   ```bash
   gcloud auth login
   ```

2. **Créer un projet** :
   ```bash
   gcloud projects create my-kubernetes-project
   gcloud config set project my-kubernetes-project
   ```

3. **Créer un cluster GKE** :
   ```bash
   gcloud container clusters create my-gke-cluster --zone us-central1-a
   ```

4. **Vérifier le cluster** :
   ```bash
   kubectl get nodes
   ```

## Suppression du cluster
   ```bash
   gcloud container clusters delete my-gke-cluster --zone us-central1-a
   ```
