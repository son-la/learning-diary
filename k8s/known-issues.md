### VXLAN issue -> pod-pod pod-service pod-apiserver communication issues
* In RHEL/ system where tcp offset is don't correctly -> Impact on VXLAN.
* Set tx offset feature off in either default interface or flannel interface.

### Container doesn't come up

* Overwrite entrypoint and shell into container for investigation
```
docker run -d --entrypoint "sh" --name test --privileged  rancher/rancher:v2.3.3 -c "tail -f /dev/null"
docker exec -it test bash
```

### Pod doesn't come up after restore from ETCD snapshot. 

* Check API server if it's spammed with authentication/ authorization issue => Delete serviceaccounttoken for service account

