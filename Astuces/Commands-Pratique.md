Create the YAML for a new ResourceQuota called 'myrq' with hard limits of 1 CPU, 1G memory and 2 pods without creating it


kubectl create quota myrq --hard=cpu=1,memory=1G,pods=2 --dry-run=client -o yaml
