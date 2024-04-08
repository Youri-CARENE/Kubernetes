kubectl run busybox --image=busybox --restart=Never --dry-run=client -o yaml --command -- env > envpod.yaml


creer juste le fichier yaml 

kubectl create namespace myns -o yaml --dry-run=client
