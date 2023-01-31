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
kubectl apply -f connectors/active/
kubectl delete -f connectors/inactive/
```

#### Cruise Control for Kafka Cluster Rebalance
```sh
# Apply the Cruise Control Rebalance Plan
kubectl apply -f cruise-control/kafka-rebalance.yaml

# Describe the Cruise Control Rebalance Plan
kubectl describe kafkarebalance kafka-cluster-rebalance

# Aprove the Cruise Control Rebalance Plan
kubectl annotate kafkarebalance kafka-cluster-rebalance strimzi.io/rebalance=approve

# Refresh to see the newest plan or info
kubectl annotate kafkarebalance kafka-cluster-rebalance strimzi.io/rebalance=refresh
```

### Creating a producer and consumer for testing porpuse
```sh

# Create a new pod called kafka-test to be a test container
kubectl run kafka-test -ti --image=quay.io/strimzi/kafka:0.32.0-kafka-3.3.1 --rm=true --restart=Never

kubectl exec kafka-test -- bin/kafka-console-producer.sh --bootstrap-server kafka-cluster-kafka-bootstrap:9092 --topic my-topic-test-json

kubectl exec kafka-test -- bin/kafka-console-consumer.sh --bootstrap-server kafka-cluster-kafka-bootstrap:9092 --topic my-topic-test-json --property print.timestamp=true --property print.key=true --from-beginning --max-messages 10

kubectl delete pod kafka-test
```

### Processing tool (ksqlDB)

```sh
# ksqlDB deployment yamls
kubectl apply -f /ksqldb/yamls/
```