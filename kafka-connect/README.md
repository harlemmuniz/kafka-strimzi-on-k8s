# Docker Build Kafka Connect Image for Strimzi
> Building an image of Kafka Connect and add drivers to ingest and consume data from different sources to Kafka

https://hub.docker.com/r/strimzi/kafka

### Build Docker image and deploy in Docker Hub
```sh
# Fazer o pull da imagem 3.3.1
docker pull quay.io/strimzi/kafka:latest-kafka-3.3.1

# Veryfing local images
docker images
strimzi/kafka

# Building Image
docker build . -t kafka-connect-strimzi:3.3.1

# Access image locally for test purpose
docker run -i -t  kafka-connect-strimzi:3.3.1 /bin/bash
cd /opt/kafka/plugins/
cd /opt/kafka/libs/

# Docker Hub (Container Images Repository)
https://hub.docker.com/repositories

# Tagging image
docker tag kafka-connect-strimzi:3.3.1 kafka-analytics/kafka-connect-strimzi:latest

# Logging in Docker Hub
docker login

# Send image to Docker Registry
docker push kafka-analytics/kafka-connect-strimzi:latest

# Remove another images
docker rmi $(docker images --filter "dangling=true" -q --no-trunc) -f
```

### Quick building in Docker Hub
```sh
docker build . -t kafka-connect-strimzi:3.3.1
docker tag kafka-connect-strimzi:3.3.1 kafka-analytics/kafka-connect-strimzi:latest
docker push kafka-analytics/kafka-connect-strimzi:latest
```

### Creating secrets with the databases credentials
```sh
# First, create a simple properties file called postgresql-credentials.properties, which should look like this:
postgres_username: postgres
postgres_password: postgres

# Create the secret:
kubectl create secret generic postgresql-credentials --from-file=./postgresql-credentials.properties
```