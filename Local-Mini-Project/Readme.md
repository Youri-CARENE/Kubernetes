Readme

Configuration de l'environnement Kubernetes local
Assurez-vous que vous avez un cluster Kubernetes fonctionnel sur votre machine locale. Vous pouvez utiliser des outils comme Minikube ou Kind pour cela.

Déploiement d'un Docker Registry
Créez un dépôt Docker Registry en exécutant le script deploy


Cela déploiera un dépôt Docker Registry avec un service exposant le port 5000.

Configuration de Jenkins
Déployez Jenkins en utilisant une configuration YAML. Voici un exemple de configuration YAML:


Cela déploiera Jenkins et exposera son interface utilisateur sur le port 8080.

Configuration de SonarQube
Déployez SonarQube en utilisant une configuration YAML. Voici un exemple de configuration YAML:

ela déploiera SonarQube et exposera son interface utilisateur sur le port 9000.

Configuration de l'application Flask
Vous pouvez utiliser une application Flask de base pour cette démonstration. Créez une application Flask et ajoutez un fichier Dockerfile avec les instructions nécessaires pour créer une image Docker pour l'application.

Configuration de la chaîne CI/CD dans Jenkins
Créez un projet Jenkins pour votre application Flask et configurez-le pour utiliser un pipeline Jenkinsfile. Le pipeline devrait inclure les étapes suivantes:

Build de l'application Flask à partir du code source.
Construction d'une image Docker








