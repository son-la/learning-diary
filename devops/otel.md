

## Tracing
* Code change using OTEL SDK to enable distributed tracing
* Auto instrument for existing application: https://grafana.com/docs/tempo/latest/getting-started/instrumentation/
* Kubernetes OTEL Operator injects instrument libraries into containers: https://opentelemetry.io/docs/kubernetes/operator/automatic/


### Propagation

* Mechanism to move data between services/ processes
* Specifications: `w3c` and `b3`  
### w3c
* Developed/ maintained by W3C
* https://www.w3.org/TR/trace-context/
* OpenTelemetry follows W3C spec, while still support `b3`

### b3
* Developed by Zipkin
* b3 concatenated: `b3: {TraceId}-{SpanId}-{SamplingState}-{ParentSpanId}`
* b3 multi: `X-B3-TraceId` and `X-B3-SpanId`

### Others
* `jaeger`, Developed by Uber with `uber-*` format

## OTEL Protocol - OTLP

* Specification https://opentelemetry.io/docs/specs/otlp/


## OTEL - Kafka
* Producer https://github.com/open-telemetry/opentelemetry-demo/blob/e5c45b9055627795e7577c395c641f6cf240f054/src/checkoutservice/main.go#L527
* Consumer https://github.com/open-telemetry/opentelemetry-demo/blob/e5c45b9055627795e7577c395c641f6cf240f054/src/accountingservice/kafka/trace_interceptor.go#L46


## Auto-instrumentation

### Supported libraries for each programming langaguage
#### Golang
* Golang autoinstrumet is not enabled. Need to add extra param: 
``` 
extraArgs:
- --enable-go-instrumentation 
```
* Gin https://pkg.go.dev/go.opentelemetry.io/contrib/instrumentation/github.com/gin-gonic/gin/otelgin

* GORM https://github.com/go-gorm/opentelemetry

* go-redis https://github.com/redis-performance/opentelemetry-go-http-sample; https://pkg.go.dev/github.com/go-redis/redis/example/otel

* sarama https://pkg.go.dev/go.opentelemetry.io/contrib/instrumentation/github.com/Shopify/sarama/otelsarama  (Deprecated)


#### Java
* Auto-instrument: https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/supported-libraries.md
#### NodeJS
* KafkaJS https://www.npmjs.com/package/opentelemetry-instrumentation-kafkajs
* Auto-instrument:  https://github.com/open-telemetry/opentelemetry-js-contrib/blob/main/metapackages/auto-instrumentations-node/README.md#supported-instrumentations

### Deployment with OTEL Operator for auto injectino
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: doraemon-producer
spec:
  replicas: 1
  selector:
    matchLabels:
      app: doraemon-producer
  template:
    metadata:
      labels:
        app: doraemon-producer
      annotations:
        sidecar.opentelemetry.io/inject: "true" # OTEL is injected as sidecar
        instrumentation.opentelemetry.io/inject-nodejs: "true" # Insturment for NodeJS
        instrumentation.opentelemetry.io/container-names: "doraemon-producer" # If there're multiple containers, select container to instrument
    spec:
      containers:
        - name: doraemon-producer
          image: doraemon:0.0.1
          imagePullPolicy: Always
          ports:
            - containerPort: 8080         
          env:
            - name: OTEL_SERVICE_NAME
              value: "doraemon-producer.app-ns"
            - name: OTEL_EXPORTER_OTLP_ENDPOINT
              value: "http://otel-collector-collector.opentelemetry-system:4317"
            - name: OTEL_EXPORTER_OTLP_INSECURE
              value: "true"
            - name: OTEL_EXPORTER_OTLP_PROTOCOL
              value: "grpc"
            - name: "OTEL_METRICS_EXPORTER"
              value: "none"
            - name: "OTEL_LOGS_EXPORTER"
              value: "none"
            
```            