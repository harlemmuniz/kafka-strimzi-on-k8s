# Apache Kafka (Strimzi Operator) & Kubernetes

### Create namespace
```sh
# create namespace
kubectl create namespace kafka-on-k8s
```

### Change current namespace
```sh
# change namespace
kubectl config set-context --current --namespace=kafka-on-k8s
```

### Add Strimzi chart & Update repositories
```sh
# add & update helm list repo
helm repo add strimzi https://strimzi.io/charts/
helm repo update
```

## Kafka-on-k8s

```sh
### Install Strimzi Operator
# strimzi
helm install kafka strimzi/strimzi-kafka-operator --version 0.31.1
```

```sh

# Create Kafka & Zookeeper Strimzi cluster with Load Balancer and storage JBOD
kubectl apply -f broker/kafka.yaml

# Create Kafka Connect Strimzi cluster
kubectl apply -f kafka-connect/kafka-connect.yaml

# Create Confluent sSchema Registry POD
helm install schema-registry cp-schema-registry
kubectl apply -f cp-schema-registry/schema-registry-service-lb.yaml

# Create Source and Sink JDBC connectors to connect with SQL Server
kubectl apply -f connectors/active/ingest-src-sqlserver-addresses-json.yaml
kubectl apply -f connectors/active/sink-sqlserver-addresses-json.yaml
kubectl delete -f connectors/inactive/enriched-src-sqlserver-addresses-json.yaml
```

### Processing

```sh
# ksqldb deployment yamls
kubectl apply -f day-3-processors/ksqldb/yamls/ -n processing

```