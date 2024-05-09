# FluxCD

* Reference architecture
    * https://github.com/fluxcd/flux2-multi-tenancy
    * https://github.com/kingdonb/bootstrap-repo/tree/main/infrastructure
    * https://github.com/son-la/gitops-reference-arch

* Patching
  * Example for patching cniBinDir of istio-cni helm release. `op:add` means adding a leaf to `cniBinDir` to the existing `cni` branch
```
patches:
  - patch: |-
      - {"op":"add","path":"/spec/values/defaults/cni/cniBinDir","value":"opt/cni/bin"}
      - {"op":"add","path":"/spec/values/defaults/cni/cniConfDir","value":"/etc/cni/net.d"}
    target:
      kind: HelmRelease
      name: istio-cni
```

* Remove/ disable
``` 
- patch: |
    $patch: delete
    apiVersion: helm.toolkit.fluxcd.io/v2beta2
    kind: HelmRelease
    metadata:
      name: removed
  target:
    kind: HelmRelease
    name: istio-cni        
        
```

* Add element to existing list. Basically replace
```
- patch: |-
    - {"op":"add","path":"/spec/rules/0/match/any/0/resources/namespaces","value":["*"]}
  target:
    kind: ClusterPolicy
    name: scale-deployment-zero
```

# GitOps testing
![alt text](system-package-cicd.drawio.png "Testing diagram")