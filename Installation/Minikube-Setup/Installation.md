# Guide d'installation de Kubernetes sur Ubuntu

Voici les étapes pour installer Kubernetes localement sur Ubuntu en utilisant Minikube :

## 1. Mise à jour des paquets

Ouvrir un terminal et mettre à jour la liste des paquets et installer les mises à jour disponibles :

``` 
sudo apt update && sudo apt upgrade -y
```

## 2. Installation des dépendances

Installer les paquets nécessaires :

``` 
sudo apt install -y apt-transport-https ca-certificates curl
```

## 3. Installation de Docker

Kubernetes utilise Docker pour exécuter les conteneurs. Pour l'installer :

``` 
# Installer Docker
```

## 4. Installation de kubectl

Kubectl est l'outil de ligne de commande pour interagir avec le cluster Kubernetes. Pour l'installer :

``` 
sudo snap install kubectl --classic
```

Vérifier l'installation :

``` 
kubectl version --client
```

## 5. Installation de Minikube

Minikube permet de créer un cluster Kubernetes local sur une machine. Pour l'installer :

``` 
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

Vérifier l'installation :

``` 
minikube version
```

## 6. Démarrage de Minikube

Démarrer Minikube en utilisant la commande suivante :

``` 
minikube start --driver=docker
```

Attendre que le processus soit terminé et que le message "Done!" s'affiche.

## 7. Vérification de l'état du cluster

Vérifier l'état du cluster Kubernetes :

``` 
minikube status
```

Si tout est correct, la sortie devrait afficher "host: Running", "kubelet: Running", et "apiserver: Running".

## 8. Utilisation de kubectl pour interagir avec le cluster

Maintenant que le cluster est opérationnel, utiliser kubectl pour interagir avec lui. Par exemple, pour afficher les nœuds du cluster, exécuter :

``` 
kubectl get nodes
```

## 9. Utilisation du tableau de bord Kubernetes (optionnel)

Minikube inclut un tableau de bord Web pour Kubernetes. Pour lancer le tableau de bord, exécuter :

``` 
minikube dashboard
```

Cette commande ouvrira le tableau de bord dans le navigateur Web par défaut.

## 10. Arrêt et suppression du cluster

Lorsque l'utilisation du cluster est terminée, arrêter le cluster :

``` 
minikube stop
```

Pour supprimer complètement le cluster et libérer des ressources, exécuter :

``` 
minikube delete
```

L'installation de Kubernetes localement sur Ubuntu en utilisant Minikube est maintenant terminée et prête à commencer à déployer des applications sur le cluster.