## Generic
* Cannot access ETCD directly

## API server
* When created with Terraform, API server is public
* Set it to private requires cluster re-creation
* Endpoints authorization can be done. Becareful not to lock yourself :)
* Once it's locked, cluster update will never finish
* To cancel long run operation:
```
az aks operation-abort --name myAKSCluster --resource-group myResourceGroup
# Ref: https://learn.microsoft.com/en-us/azure/aks/manage-abort-operations?tabs=azure-cli
```
* Applying change with az cli
```
az aks update --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges 73.140.245.0/24
# Ref: https://learn.microsoft.com/en-us/azure/aks/api-server-authorized-ip-ranges?tabs=azure-cli
```

## Debug node
```
kubectl debug node/aks-nodepool1-37663765-vmss000000 -it --image=mcr.microsoft.com/cbl-mariner/busybox:2.0
# Ref: https://learn.microsoft.com/en-us/azure/aks/node-access
```