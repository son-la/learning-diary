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

## Benefit of OCI registry for GitOps

* Pulling an OCI image is a much less resource-intensive process compared to cloning a Git repository, making it more efficient for deployment purposes.
* High available registries are easier to deploy than Git servers, making it easy to access and deploy container images from any location.
* OCI repositories can scale out similarly to a Content Delivery Network, enabling platform team to distribute configurations globally with ease.
* Flux uses Kubernetes workload identity and IAM to pull OCI artifacts from managed registries. This eliminates the need for key management, SSH key generation, and proprietary * API usage for token generation. Instead, the same mechanism used for pulling container images for applications is used.
* OCI images can be signed and verified during container deployment. Flux supports these verifications, out of the box.
* REF : https://sestegra.medium.com/gitops-with-flux-leveraging-oci-registry-as-a-state-store-ffe28dd64836