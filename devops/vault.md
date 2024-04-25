## General


* Storage
  * Integrated storage: Raft (Like ETCD)
  * External storage:
* Requests are directed to leader instance to handle read/write request. Extra hop is made in the network if DNS loadbalancer is done (no way to now which one is leader)
* Unseal
  * Unseal is required when vault is sealed (e.g.: after node's reboot, service restart)
  * Unseal requires 3/5 unseal keys
  * Login to each sealed vault node/ from UI
  * Setup auto unseal
* Healthcheck
  * /v1/sys/health
* Snapshot
  * `https://github.com/sidicer/vault-snapshot.sh`

* Restore
  * `https://developer.hashicorp.com/vault/tutorials/standard-procedures/sop-restore`