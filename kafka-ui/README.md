# Install Kafka-UI
```bash

helm install -kafka-ui . --namespace kafka-on-k8s \
--set envs.config.KAFKA_CLUSTERS_0_NAME=kafka-cluster \
--set envs.config.KAFKA_CLUSTERS_0_BOOTSTRAPSERVERS=kafka-cluster-kafka-bootstrap.kafka-on-k8s.svc.cluster.local:9092 \
--set envs.config.KAFKA_CLUSTERS_0_SCHEMAREGISTRY=http://schema-registry-cp-schema-registry.kafka-on-k8s.svc.cluster.local:8081 \
--set envs.config.KAFKA_CLUSTERS_0_KAFKACONNECT_0_NAME=connect-cluster \
--set envs.config.KAFKA_CLUSTERS_0_KAFKACONNECT_0_ADDRESS=http://connect-cluster-connect-api.kafka-on-k8s.svc.cluster.local:8083
# --set envs.config.KAFKA_CLUSTERS_0_KSQLDBSERVER=ksqldb-server.processing.svc.cluster.local:8088
```