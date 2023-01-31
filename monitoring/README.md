## Installing Prometheus CoreOs operator

Search for all "namespace: " in prometheus-operator-deployment.yaml and substitute for your namespace, ex.: kafka-on-k8s

```bash
# Deploy the Prometheus Operator:
kubectl create -f prometheus-operator-deployment.yaml
```

## Deploying Prometheus

```bash
# Change the namespace in prometheus.yaml;

# Edit the PodMonitor in strimzi-pod-monitor.yaml in namespaceSelector > matchNames to match the namespace set in prometheus.yaml;

# Create a Secret resource from the configuration file prometheus-additional-properties/prometheus-additional.yaml:
kubectl apply -f prometheus-additional-properties/prometheus-additional.yaml

# Deploy the Prometheus resources:
kubectl apply -f prometheus-install/strimzi-pod-monitor.yaml
kubectl apply -f prometheus-install/prometheus-rules.yaml
kubectl apply -f prometheus-install/prometheus.yaml

# Use port-forward to redirect Prometheus UI to localhost:9090:
kubectl port-forward svc/prometheus-operated 9090:9090
```

## Deploying Alertmanager

```bash
# Update the prometheus-alertmanager-config/alert-manager-config.yaml:
  # slack_api_url: put your Slack API URL related to Slack Workplace
  # channel: the channel property in your Slack to send notifications

# Create a Secret resource from the configuration file prometheus-alertmanager-config/alert-manager-config.yaml:
kubectl apply -f prometheus-alertmanager-config/alert-manager-config.yaml

# Deploy the Alertmanager:
kubectl apply -f prometheus-install/alert-manager.yaml
```

## Deploying Grafana

```bash
# Deploy Grafana:
kubectl apply -f grafana-install/grafana.yaml

# Get details of the Grafana service:
kubectl get svc grafana

# Use port-forward to redirect Grafana UI to localhost:3000:
kubectl port-forward svc/grafana 3000:3000

# Open the web browser and access grafana using the url http://localhost:3000.

# Enter the user name and password and click in Log In
  # The default username and password are both admin. After logging in for the first time, it's possible to change the password.

# In Configuration > Data Sources, add Prometheus as data source
  # Choose a name;
  # Add Prometheus as type;
  # Specify the Prometheus server URL: http://prometheus-operated:9090
  # Save and test the connection

# In the + button, click in Import and import the grafana dashboards located in grafana-dashboard

```