# Install Kafka-UI
```bash
# Create the config map to point Kafka-UI to kafka cluster
kubectl apply -f ./kafka-ui/kafka-ui-config-map.yaml

# Create a network policy to allow Kafka-UI to use the REST API for Kafka Connect
kubectl apply -f ./kafka-ui/kafka-ui-network-policy.yaml

# Install the Kafka-UI chart
helm install kafka-ui ./kafka-ui --set existingConfigMap="kafka-ui-config-map"

# Point the localhost:8080 to kafka-ui:80, and open http://localhost:8080
kubectl port-forward svc/kafka-ui 8080:80

or

export POD_NAME=$(kubectl get pods -n namespace -l "app.kubernetes.io/name=kafka-ui,app.kubernetes.io/instance=kafka-ui" -o jsonpath="{.items[0].metadata.name}")

kubectl port-forward $POD_NAME 8080:80 -n namespace
```