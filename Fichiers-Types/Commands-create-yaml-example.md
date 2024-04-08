kubectl run busybox --image=busybox --restart=Never --dry-run=client -o yaml --command -- env > envpod.yaml


# creer juste le fichier yaml 

kubectl create namespace myns -o yaml --dry-run=client


# Create a pod with an nginx container exposed on port 80

kubectl run box --image=nginx --restart=Never --port=80 --dry-run=client -o yaml > pod-init.yaml
