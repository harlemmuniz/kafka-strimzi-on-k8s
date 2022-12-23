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
docker tag kafka-connect-strimzi:3.3.1 harlemmuniz/kafka-connect-strimzi:3.3.1

# Logging in Docker Hub
docker login

# Send image to Docker Registry
docker push harlemmuniz/kafka-connect-strimzi:3.3.1

# Remove another images
docker rmi $(docker images --filter "dangling=true" -q --no-trunc) -f
```

### Quick building in Docker Hub
```sh
docker build . -t kafka-connect-strimzi:3.3.1
docker tag kafka-connect-strimzi:3.3.1 harlemmuniz/kafka-connect-strimzi:3.3.1
docker push harlemmuniz/kafka-connect-strimzi:3.3.1
```