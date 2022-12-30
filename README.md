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

### Add Strimzi chart, update repositories & install Strimzi Operator
```sh
# add & update helm list repo
helm repo add strimzi https://strimzi.io/charts/
helm repo update
helm install kafka strimzi/strimzi-kafka-operator --version 0.32.0
```

## Kafka-on-k8s
```sh

# Create Kafka & Zookeeper Strimzi cluster with Load Balancer and storage JBOD
kubectl apply -f broker/kafka.yaml

# Create Kafka Connect Strimzi cluster
kubectl apply -f kafka-connect/kafka-connect.yaml

# Create Kafka topics
kubectl apply -f topic/src-sqlserver-addresses-json.yaml

# Create Confluent Schema Registry POD
helm install schema-registry cp-schema-registry
kubectl apply -f cp-schema-registry/schema-registry-service-lb.yaml

# Create/Delete Source and Sink JDBC connectors to connect with SQL Server
kubectl apply -f connectors/active
kubectl delete -f connectors/inactive
```

#### Cruise Control for Kafka Cluster Rebalance
```sh
# Apply the Cruise Control Rebalance Plan
kubectl apply -f cruise-control/kafka-rebalance.yaml

# Describe the Cruise Control Rebalance Plan
kubectl describe kafkarebalance kafka-cluster-rebalance -n kafka-analytics

# Aprove the Cruise Control Rebalance Plan
kubectl annotate kafkarebalance kafka-cluster-rebalance strimzi.io/rebalance=approve -n kafka-analytics

# Refresh to see the newest plan or info
kubectl annotate kafkarebalance kafka-cluster-rebalance strimzi.io/rebalance=refresh -n kafka-analytics
```

### Processing tool (ksqlDB)

```sh
# ksqlDB deployment yamls
kubectl apply -f /ksqldb/yamls/
```
