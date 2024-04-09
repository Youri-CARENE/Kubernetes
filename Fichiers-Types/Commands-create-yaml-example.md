kubectl run busybox --image=busybox --restart=Never --dry-run=client -o yaml --command -- env > envpod.yaml


# creer juste le fichier yaml 

kubectl create namespace myns -o yaml --dry-run=client


# Create a pod with an nginx container exposed on port 80

kubectl run box --image=nginx --restart=Never --port=80 --dry-run=client -o yaml > pod-init.yaml


# Create a configmap named config with values foo=lala,foo2=lolo
kubectl create configmap config --from-literal=foo=lala --from-literal=foo2=lolo

# Create a configmap from a file
kubectl create cm configmap2 --from-file=config.txt

# Create and display a configmap from a .env file
kubectl create cm configmap3 --from-env-file=config.env


# General Create a configMap 'type' with values 'var8=val8', 'var9=val9
kubectl create configmap type-name --from-literal=var8=val8 --from-literal=var9=val9
