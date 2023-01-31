# Install Kafka-UI
```bash
kubectl apply -f ./kafka-ui/kafka-ui-config-map.yaml

helm install kafka-ui ./kafka-ui --set existingConfigMap="kafka-ui-config-map"

kubectl port-forward svc/kafka-ui 8080:80
```