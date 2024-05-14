
## K3D

* k3d bootstrap k3s cluster
* fluxcd to re-deploy applications
* chainsaw for e2e testing


* Start cluster with 1 server, 3 agents, no traefik, with port mapping for nodeport
```
k3d cluster create test-cluster --servers 1 --agents 3 -p "30000-30100:30000-30100@server:0"
```

* TODO: Study metallb

* Issue with k3d and vpn
```
# https://github.com/k3d-io/k3d/issues/1017
export K3D_FIX_DNS=1
```

* Issue with kubecost frontend https://github.com/opencost/opencost/issues/2465 Seems that k3d doesn't support ipv6 by default? Or is it because my laptop's IPv6 is disabled?

## Kind

* https://kind.sigs.k8s.io/docs/user/quick-start/#installing-from-release-binaries
* Advantages:
  * Well integrated with k8s e2e framework

### Installation
``` 
# For AMD64 / x86_64
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.22.0/kind-linux-amd64
# For ARM64
[ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.22.0/kind-linux-arm64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

* Increase open file limits
```
# /etc/sysctl.conf
# ref: https://www.suse.com/support/kb/doc/?id=000020048
fs.inotify.max_user_instances=8192
fs.inotify.max_user_watches=524288
```