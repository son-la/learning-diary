---
layout: page
title: "EKS"
---

* Design arch for ip reservation https://aws.amazon.com/blogs/containers/addressing-ipv4-address-exhaustion-in-amazon-eks-clusters-using-private-nat-gateways/ 



### Autoscaling
https://karpenter.sh/

### Storage
ReadWriteOnce, ebs-csi: https://github.com/kubernetes-sigs/aws-ebs-csi-driver
ReadWriteMany, efs-csi: https://github.com/kubernetes-sigs/aws-efs-csi-driver/tree/master