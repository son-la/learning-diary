
* k3d bootstrap k3s cluster
* fluxcd to re-deploy applications
* chainsaw for e2e testing


* Start cluster with 1 server, 3 agents, no traefik, with port mapping for nodeport
```
k3d cluster create test-cluster --servers 1 --agents 3 -p "30000-30100:30000-30100@server:0"
```

* TODO: Study metallb


* Issue with kubecost frontend https://github.com/opencost/opencost/issues/2465 Seems that k3d doesn't support ipv6 by default? Or is it because my laptop's IPv6 is disabled?