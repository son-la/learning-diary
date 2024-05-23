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



## Troubleshooting

### init-container network connectivity
* `holdApplicationUntilProxyStarts` makes istio containers to the first place, still `istio-proxy` sidecar container doesn't start until app's init-container start.
* If app's init-container requires connecvity, this will not work 
* By setting init-container user to 1337, its traffic will not be filtered by iptable
* Other option is to change init-container to be sidecar container and relying on how kubelet starts container to make sure `istio-proxy -> sidecar container (previously init container) -> main container`. Ref: https://medium.com/@marko.luksa/delaying-application-start-until-sidecar-is-ready-2ec2d21a7b74
  
   