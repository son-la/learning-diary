# Get deployment/ statefulset with certain annotations
```
kubectl get statefulset --all-namespaces -o json | jq -r '.items[] | select(.metadata.annotations["sre.corp.org/troubleshooting-needed"] == "true") | {namespace: .metadata.namespace, name: .metadata.name}'

kubectl get deployments --all-namespaces -o json | jq -r '.items[] | select(.metadata.annotations["sre.corp.org/troubleshooting-needed"] == "true") | {namespace: .metadata.namespace, name: .metadata.name}'
```
