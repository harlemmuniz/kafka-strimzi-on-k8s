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