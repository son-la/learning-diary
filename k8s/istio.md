## Gateway
* istio-ingress can be exposed via either svc of type Nodeport or 
Loadbalancer
* Support mTLS out of the box among services

## Virtual service
* loadbalance incoming traffics to different deployments. E.g.: 90% to first deployment, 10% to second deployment 
* rule based on header value 

* fault injection

## Istio cni
* `istio-cni` needs to be enabled in `istiod`

## Certificate management
TODO: Read https://tetrate.io/blog/how-are-certificates-managed-in-istio/

* Brings own CA when needs to setup meshes spanning multiple clusters
## Ambient mode
* Beta mode March 2024

## OTEL integration

### Distributed tracing
* Provided by Envoy
* Ingress and Egress spans for each service

### Access log
* Proivded by Envoy
* Ingress log only
* By default -> stdout
* Istio can export OTLP Enovy access logs via either gRPC or HTTP to OTEL collector
* Access log is enabled -> Tracing spans are combined into single trace.

## Troubleshooting

### init-container network connectivity
* `holdApplicationUntilProxyStarts` makes istio containers to the first place, still `istio-proxy` sidecar container doesn't start until app's init-container start.
* If app's init-container requires connecvity, this will not work 
* By setting init-container user to 1337, its traffic will not be filtered by iptable
* Other option is to change init-container to be sidecar container and relying on how kubelet starts container to make sure `istio-proxy -> sidecar container (previously init container) -> main container`. Ref: https://medium.com/@marko.luksa/delaying-application-start-until-sidecar-is-ready-2ec2d21a7b74
  
   