Ouvrez un terminal et exécutez la commande suivante pour mettre à jour la liste des paquets et installer les mises à jour disponibles:

 
sudo apt update && sudo apt upgrade -y
Installer les dépendances:
Installez les paquets nécessaires avec la commande suivante:

 
sudo apt install -y apt-transport-https ca-certificates curl
Installer Docker:
Kubernetes utilise Docker pour exécuter les conteneurs. Installez Docker en suivant les étapes de la documentation d'installation de Docker pour Ubuntu dans la réponse précédente.

Installer kubectl:
Kubectl est l'outil de ligne de commande pour interagir avec le cluster Kubernetes. Installez kubectl en utilisant la commande suivante:
 
sudo snap install kubectl --classic
Vérifiez l'installation en exécutant:

 
kubectl version --client
Installer Minikube:
Minikube vous permet de créer un cluster Kubernetes local sur votre machine. Installez Minikube en utilisant la commande suivante:

 
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
Vérifiez l'installation en exécutant:

 
minikube version
Démarrer Minikube:
Démarrez Minikube en utilisant la commande suivante:

 
minikube start --driver=docker
Cette commande démarre Minikube en utilisant le pilote Docker. Attendez que le processus soit terminé et que le message "Done!" s'affiche.

Vérifier l'état du cluster:
Vérifiez l'état du cluster Kubernetes en utilisant la commande suivante:

 
minikube status
Si tout est correct, vous devriez voir "host: Running", "kubelet: Running", et "apiserver: Running" dans la sortie.

Utiliser kubectl pour interagir avec le cluster:
Maintenant que votre cluster est opérationnel, utilisez kubectl pour interagir avec lui. Par exemple, pour afficher les nœuds du cluster, exécutez:

 
kubectl get nodes
Utiliser le tableau de bord Kubernetes (optionnel):
Minikube inclut un tableau de bord Web pour Kubernetes. Pour lancer le tableau de bord, exécutez:

 
minikube dashboard
Cette commande ouvrira le tableau de bord dans votre navigateur Web par défaut.

Arrêter et supprimer le cluster:
Lorsque vous avez terminé d'utiliser le cluster, arrêtez-le en exécutant:

 
minikube stop
Pour supprimer complètement le cluster et libérer des ressources, exécutez:

 
minikube delete
Vous avez maintenant installé Kubernetes localement sur Ubuntu en utilisant Minikube et êtes prêt à commencer à déployer des applications sur votre cluster.