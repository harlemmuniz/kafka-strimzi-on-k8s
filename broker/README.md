## Deploy Kafka Brokers, Zookeeper Nodes, ConfigMaps to get metrics and Services to Kafka and Zookeeper communication

```sh
# Create Kafka & Zookeeper Strimzi cluster with Load Balancer and storage JBOD
kubectl apply -f broker/kafka.yaml
```