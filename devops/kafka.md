

* Parameters can be global or per topic
* KAFKA_CFG_TRANSACTION_STATE_LOG_MIN_ISR = 1 means 1 broker (leader) needs to ack the message is put to queue
* KAFKA_CFG_TRANSACTION_STATE_LOG_MIN_ISR = 2 means 2 broker (leader) needs to ack the message is put to queue. Cluster must have at least 3, to even tolerates 1 broker failure

## Kafka client testing

* Create broker config file
```
# Username and password for sasl/scram auth type 
sasl.jaas.config=org.apache.kafka.common.security.scram.ScramLoginModule required username="x" password="x";

# Truststore for cluster ca
ssl.truststore.location=/home/sonla/Downloads/kafka.client.truststore.jks
ssl.truststore.password=kafkax

# As specified in authentcation method in Kafka listener configuration
security.protocol=SASL_SSL
sasl.mechanism=SCRAM-SHA-512

# This is to bypass hostname verification since connection is made outside of cluster for temporary verification
# ssl.endpoint.identification.algorithm=
```


```
# Create topic
./kafka-topics.sh --bootstrap-server localhost:30001 --create --topic test --command-config config.properties

# Delete topic
./kafka-topics.sh --bootstrap-server localhost:30001 --delete --topic test --command-config config.properties

# Describe topic
./kafka-topics.sh --bootstrap-server https://localhost:30001 --describe --topic test --command-config config.properties

# Consume topic
./kafka-console-consumer.sh  --bootstrap-server  localhost:30001 --consumer.config config.properties --topic test  --from-beginning
```



### Truststore
```
# Look for `<cluster-name>-cluster-ca-cert`
kubectl get secrets/kafka-cluster-clients-ca-cert -n kafka -o jsonpath="{.data.ca\.crt}" | base64 -d > ca.crt
keytool -importcert -file ca.crt -keystore kafka.client.truststore.jks -storepass kafkax -alias CARoot
```

