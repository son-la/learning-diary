
* k3d bootstrap k3s cluster
* fluxcd to re-deploy applications
* chainsaw for e2e testing


* Start cluster with 1 server, 3 agents, no traefik, with port mapping
```
k3d cluster create test-cluster --servers 1 --k3s-arg '--disable=servicelb@server:*'  --k3s-arg '--disable=traefik@server:*'
```


* Issue with k3d and vpn
```
# https://github.com/k3d-io/k3d/issues/1017
export K3D_FIX_DNS=1
```

* Issue with kubecost frontend https://github.com/opencost/opencost/issues/2465 Seems that k3d doesn't support ipv6 by default? Or is it because my laptop's IPv6 is disabled?