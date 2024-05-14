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


# Golang K8S SIG e2e framework

## Overview

* Use Golang test stdlib to manage test execution
* Very well integrate with other Kubernetes projects. For example FluxCD:
```
import (
  ...
	kustomizev1 "github.com/fluxcd/kustomize-controller/api/v1"
  ...
)

func WaitForHelmKustomizationToBeReady(name string, namespace string, timeoutInMinute int, ctx context.Context, t *testing.T, r *resources.Resources) error {
	kustomizev1.AddToScheme(r.GetScheme())
	kustomization := &kustomizev1.Kustomization{}

	if err := r.Get(ctx, name, namespace, kustomization); err != nil {
		t.Logf("Error getting resource %v\n", err)
		t.Fatal("Could not get resource")
		return err
	}

	if err := wait.For(conditions.New(r).ResourceMatch(kustomization, func(object k8s.Object) bool {
		d := object.(*kustomizev1.Kustomization)
		return meta.IsStatusConditionTrue(d.Status.Conditions, apimeta.ReadyCondition)
	}), wait.WithTimeout(time.Minute*time.Duration(timeoutInMinute))); err != nil {
		t.Fatalf("Timeout waiting for Kustomization %s/%s to be ready. Error: %v\n", namespace, name, err)
		return err
	}

	return nil
}


```