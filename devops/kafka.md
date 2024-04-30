

* Parameters can be global or per topic
* KAFKA_CFG_TRANSACTION_STATE_LOG_MIN_ISR = 1 means 1 broker (leader) needs to ack the message is put to queue
* KAFKA_CFG_TRANSACTION_STATE_LOG_MIN_ISR = 2 means 2 broker (leader) needs to ack the message is put to queue. Cluster must have at least 3, to even tolerates 1 broker failure