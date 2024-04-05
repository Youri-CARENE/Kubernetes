Si vous ne recevez pas de fichier de définition de pod, vous pouvez extraire la définition dans un fichier à l'aide de la commande ci-dessous :

```bash
kubectl get pod <pod-name> -o yaml > pod-definition.yaml
```

Modifiez ensuite le fichier pour apporter les modifications nécessaires, supprimez et recréez le pod.

Pour modifier les propriétés du pod, vous pouvez utiliser la commande `kubectl edit pod <pod-name>`. Veuillez noter que seules les propriétés répertoriées ci-dessous sont modifiables.

- `spec.containers[*].image`
- `spec.initContainers[*].image`
- `spec.activeDeadlineSeconds`
- tolérances `spec.`
- `spec.terminationGracePeriodSeconds`
