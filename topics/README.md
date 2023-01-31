# To create a new topic

1. **Create the yaml file**, following a model inside the models folder;

2. **Put it in active folder**;

3. **Execute the following code** to create it inside Apache Kafka brokers:
    ```bash
    kubectl apply -f topics/active/topic-name.yaml
    ```