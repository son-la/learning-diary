# Chainsaw


## Overview
* Designed to test Kubernetes operator/ controllers in a declarative approach
* Current version is 0.2.0
* Kubernetes operator works usually that:
  * 1. Operator is running 
  * 2. User deploys CR
  * 3. Operator checks CR and perform Create/ Update of actual resources according ly

## Installation
* Download chainsaw binary from https://github.com/kyverno/chainsaw/releases
* Setup test cluster locally e.g.: minikube, k3s, k3d, ...

## Concepts
### Test
* Sequences of test steps

### Test step
* List of operations: https://kyverno.github.io/chainsaw/latest/steps/
* `Delete`, `Create`, or `Assert` a resource in the cluster
* Run abitrary command or scripts

### Cleanup
* Cleanup happens by default. First created -> Last deleted