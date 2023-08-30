# Schema Registry

Created by Confluent, the Schema Registry give a service layer to keep message metadatas. It's provides a **RESTFul interface to store and retrieve Avro, JSON and Protobuf schemas**, and uses its Apache Kafka protocol as a storage layer.

<<<<<<< HEAD
=======
## Instalation

```bash
# Create Confluent Schema Registry POD
helm install schema-registry cp-schema-registry

# OPTIONAL: Schema Registry Load Balancer
kubectl apply -f cp-schema-registry/schema-registry-service-lb.yaml
```

>>>>>>> 26f404222602c26e8104aea59bc6116b451a3f9a
## Working with Schema Registry
    
   Change the **localhost to the external ip from Schema Registry Service**, the **schema name** and **version**.
    
- **List all subjects**
        
    ```bash
    curl -X GET http://localhost:8081/subjects
    ```

- **Register a new schema version to a subject**
        
    ```bash
    curl -X POST -H "Content-Type: application/vnd.schemaregistry.v1+json" \
<<<<<<< HEAD
        --data '{ \"type\": \"record\", \"name\": \"table_one\", \"namespace\": \"com.analytics\", \"fields\": [{ \"name\": \"id_table_one\", \"type\": [\"null\", \"int\"], \"default\": null }, { \"name\": \"description_table_one\", \"type\": [\"null\", \"string\"], \"default\": null }] }' \
=======
        --data '{ \"type\": \"record\", \"name\": \"tipo_motivo_negociacao\", \"namespace\": \"com.kafkatest\", \"fields\": [{ \"name\": \"id_tipo_motivo_negociacao\", \"type\": [\"null\", \"int\"], \"default\": null }, { \"name\": \"tx_tipo_motivo_negociacao\", \"type\": [\"null\", \"string\"], \"default\": null }] }' \
>>>>>>> 26f404222602c26e8104aea59bc6116b451a3f9a
        http://localhost:8081/subjects/src-postgresql-handshake-avro/versions
    ```

- **List all schema versions** from a subject
        
    ```bash
    curl -X GET http://localhost:8081/subjects/src-postgresql-handshake-avro/versions
    ```

- **Searching the version 1 from a schema**
    
    ```bash
    curl -X GET http://**localhost**:8081/subjects/**src-postgresql-handshake-avro**/versions/**1**
    ```

- **Deleting the version 1** of a schema
        
    ```bash
    curl -X DELETE http://localhost:8081/subjects/src-postgresql-handshake-avro/versions/1
    ```

- **Checking if there is a schema created** to a subject
        
    ```bash
    curl -X POST -H "Content-Type: application/vnd.schemaregistry.v1+json" \
        --data '{"schema": "{\"type\": \"string\"}"}' \
        http://localhost:8081/subjects/src-postgresql-handshake-avro
    ```

PS.: The Connector create schemas automatically.