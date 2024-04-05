# Modification de Pods et Deployments

## Éditer un POD

Il est important de se rappeler que vous **ne pouvez PAS** éditer les spécifications d'un POD existant, à l'exception des champs suivants :

- `spec.containers[*].image`
- `spec.initContainers[*].image`
- `spec.activeDeadlineSeconds`
- `spec.tolerations`

Par exemple, vous ne pouvez pas éditer les variables d'environnement, les comptes de service, les limites de ressources d'un pod en cours d'exécution. Si vous devez vraiment apporter des modifications, vous avez deux options :

### Option 1 : Utilisation de `kubectl edit pod`

1. Exécutez la commande `kubectl edit pod <nom du pod>`. Cela ouvrira la spécification du pod dans un éditeur (éditeur vi). Ensuite, éditez les propriétés requises. Lorsque vous essayez de sauvegarder, vous serez refusé car vous tentez de modifier un champ du pod qui n'est pas modifiable.

   Un copie du fichier avec vos changements est sauvegardée dans un emplacement temporaire.

2. Vous pouvez ensuite supprimer le pod existant en exécutant la commande :

   ```bash
   kubectl delete pod webapp
   ```

3. Puis créez un nouveau pod avec vos changements en utilisant le fichier temporaire :

   ```bash
   kubectl create -f /tmp/kubectl-edit-ccvrq.yaml
   ```

### Option 2 : Extraction et Modification du Définition du Pod

1. Extrayez la définition du pod au format YAML dans un fichier en utilisant la commande :

   ```bash
   kubectl get pod webapp -o yaml > my-new-pod.yaml
   ```

2. Faites ensuite les changements dans le fichier exporté en utilisant un éditeur (éditeur vi). Sauvegardez les changements.

   ```bash
   vi my-new-pod.yaml
   ```

3. Supprimez ensuite le pod existant :

   ```bash
   kubectl delete pod webapp
   ```

4. Puis créez un nouveau pod avec le fichier édité :

   ```bash
   kubectl create -f my-new-pod.yaml
   ```

## Éditer des Deployments

Avec les Deployments, vous pouvez facilement éditer n'importe quel champ/propriété du template de POD. Puisque le template de pod est un enfant de la spécification de déploiement, à chaque changement, le déploiement supprimera automatiquement et créera un nouveau pod avec les nouveaux changements. Si vous êtes invité à éditer une propriété d'un POD faisant partie d'un déploiement, vous pouvez simplement le faire en exécutant la commande :

```bash
kubectl edit deployment mon-deploiement
```

Cette commande ouvre la spécification du déploiement dans un éditeur, permettant de modifier facilement et de manière déclarative n'importe quelle partie de la spécification du pod.
