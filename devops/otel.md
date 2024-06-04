

## Tracing
* Code change using OTEL SDK to enable distributed tracing
* Auto instrument for existing application: https://grafana.com/docs/tempo/latest/getting-started/instrumentation/
* Kubernetes OTEL Operator injects instrument libraries into containers: https://opentelemetry.io/docs/kubernetes/operator/automatic/


## OTEL Protocol - OTLP

* Specification https://opentelemetry.io/docs/specs/otlp/


## OTEL - Kafka
* Producer https://github.com/open-telemetry/opentelemetry-demo/blob/e5c45b9055627795e7577c395c641f6cf240f054/src/checkoutservice/main.go#L527
* Consumer https://github.com/open-telemetry/opentelemetry-demo/blob/e5c45b9055627795e7577c395c641f6cf240f054/src/accountingservice/kafka/trace_interceptor.go#L46