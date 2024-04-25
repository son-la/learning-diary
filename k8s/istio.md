## Gateway
* istio-ingress can be exposed via either svc of type Nodeport or 
Loadbalancer
* Support mTLS out of the box among services

## Virtual service
* loadbalance incoming traffics to different deployments. E.g.: 90% to first deployment, 10% to second deployment 
* rule based on header value 

* fault injection


## Tracing
* Application must use OTEL 


## Storage
* Cassandra