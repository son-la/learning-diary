---
layout: page
title: "EKS"
---

* Design arch for ip reservation https://aws.amazon.com/blogs/containers/addressing-ipv4-address-exhaustion-in-amazon-eks-clusters-using-private-nat-gateways/ 


### Loadbalancer
* NLB with TLS termination https://aws.amazon.com/blogs/aws/new-tls-termination-for-network-load-balancers/
* Let's Encrypt + cert-manager: https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/set-up-end-to-end-encryption-for-applications-on-amazon-eks-using-cert-manager-and-let-s-encrypt.html
* ELB -> EKS's Nginx Ingress can be TLS with self-signed cert

### Autoscaling
https://karpenter.sh/

* Karpenter Terraform module
  > * Node role: For Karpenter scaled node
  > * Controller role: For Karpenter controller (deployed on Kubernetes)
  > * Access control: Allow Node role to access EKS's API. Otherwise, manually modify aws-auth configmap

### Storage
ReadWriteOnce, ebs-csi: https://github.com/kubernetes-sigs/aws-ebs-csi-driver
ReadWriteMany, efs-csi: https://github.com/kubernetes-sigs/aws-efs-csi-driver/tree/master