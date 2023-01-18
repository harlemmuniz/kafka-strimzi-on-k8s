## Creating the secrets with the database credential

1. In your machine create a simple yaml file called postgresql-credentials.yaml, containing the database credentials and url, inside the connector.properties:

    ```yaml
    apiVersion: v1
    kind: Secret
    metadata:
      name: postgresql-credentials
    type: Opaque
    stringData:
      connector-postgresql.properties: |- 
        postgres_username: postgres_username
        postgres_password: postgres_password
        postgres_url: jdbc:postgresql://localhost:5432/dbname
    ```
    - **metadata.name**: name of the secret to be imported by the volume;
    - **stringData.connector.properties**: name of the volume containing the secret to be created.
    
2. Create the secret:

    ```sh
    kubectl apply -f secrets/postgresql-credentials.yaml
    ```

## Create the volume to mount the Secrets to the Kafka Connect Pod

1. Configure the kafka-connect.yaml to create volumes and set secret values
    ```yaml
    spec:
    # ...
    config:
        config.providers: file
        config.providers.file.class: org.apache.kafka.common.config.provider.FileConfigProvider
    #...
    externalConfiguration:
        volumes:
        - name: connector-postgresql-config
            secret:
            secretName: postgresql-credentials
    ```
    - **config.config.providers**: alias for the configuration provider;
    - **config.config.providers.file.class**: FileConfigProvider provides values from properties files (the Secret);
    - **externalConfiguration.volumes.name**: (stringData.connector.properties) name of the volume containing the secret;
    - **externalConfiguration.volumes.name.secret.secretName**: metadata.name (postgresql-credentials) of the secret created.

## Use the secret values created inside the Connectors

1. Set the property values in the connector configuration

    The structure is: "${file:/opt/kafka/external-configuration/**VOLUME-NAME**/**SECRET-NAME**.properties:**PROPERTY-NAME**}"

    ```yaml
    spec:
        class: io.confluent.connect.jdbc.JdbcSourceConnector
        tasksMax: 2
        config:
            #...
            connection.url: "${file:/opt/kafka/external-configuration/connector-postgresql-config/postgresql-credentials.properties:postgres_url}"
            connection.user: "${file:/opt/kafka/external-configuration/connector-postgresql-config/postgresql-credentials.properties:postgres_username}"
            connection.password: "${file:/opt/kafka/external-configuration/connector-postgresql-config/postgresql-credentials.properties:postgres_password}"
            #...
    ```

## DON'T DEPLOY THE SECRET YAML FILES