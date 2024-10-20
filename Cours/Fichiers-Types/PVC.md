Create a PersistentVolumeClaim for this storage class, called 'mypvc', a request of 4Gi and an accessMode of ReadWriteOnce, with the storageClassName of normal, and save it on pvc.yaml. Create it on the cluster. Show the PersistentVolumeClaims of the cluster. Show the PersistentVolumes of the cluster
show



``` yaml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: mypvc
spec:
  storageClassName: normal
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 4Gi

```

 # create it

kubectl create -f pvc.yaml


# Show the PersistentVolumeClaims and PersistentVolumes:

kubectl get pvc # will show as 'Bound'
kubectl get pv # will show as 'Bound' as well
