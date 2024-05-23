# Mutual TLS

## Requriements
* Identity
    > * *Identity validation* is the process to validate application workload identity by a well-known, trusted authority
    > * Identity needs to be cryptographically verifiable
* Confidentiality
    > * Communication channel is encrypted uniqly for 2 parties (prevent man-in-the-middle attack, confused deputy problem)

* Integrity
    > * Transfered data is not modified by any other identity than source/ destination

* Access policy enforcement
    > * Standard TLS only verifies server side i.e.: The server is trusted
    > * Cryptographically verifiable identity for both end of the communication

## TLS 1.3
* Server side is authenticated. Client side authentication is optional
* Unique session key is generated for particular server and client communication




## Ref
* https://istio.io/latest/blog/2023/secure-apps-with-istio/
