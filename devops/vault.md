## General


* Storage
  * Integrated storage: Raft (Like ETCD)
  * External storage:
* Requests are directed to leader instance to handle read/write request. Extra hop is made in the network if DNS loadbalancer is done (no way to now which one is leader)
* Unseal
  * Unseal is required when vault is sealed (e.g.: after node's reboot, service restart)
  * Unseal requires 3/5 unseal keys
  * Login to each sealed vault node/ from UI
  * Auto unseal with Azure Key Vault
    * Service principal is created and allow access to Key Vault with `Key Vault Crypto User` role
    * Azure KV is configured on `/etc/vault.d/vault.hcl` of each instance
    * If Vault was initizilied, seal migration process is needed

* AD integration.
  * Creating Service principal in Azure and configure client_id and client_secret
  * Rotate client_secret every 1 yr

* Healthcheck
  * /v1/sys/health
* Snapshot
  * `https://github.com/sidicer/vault-snapshot.sh`

* Restore
  * `https://developer.hashicorp.com/vault/tutorials/standard-procedures/sop-restore`
 

 ## Vault policy
 * Becareful with multiple policies: https://github.com/hashicorp/vault/issues/3892. More specific/ longer path takes over shorter (wildcard) one. 
