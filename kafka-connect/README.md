# Docker Build Kafka Connect Image for Strimzi
> building a new image to add the extra connectors and drivers to ingest data from different sources to kafka

https://hub.docker.com/r/strimzi/kafka

### build image and deploy hub
```sh
# Fazer o pull da imagem 3.2.3
docker pull quay.io/strimzi/kafka:latest-kafka-3.2.3

# Verificar as imagens locais
docker images
strimzi/kafka

# Buildar a imagem
docker build . -t jdbc-kafka-connect-strimzi:3.2.3

# Acessar a imagem
docker run -i -t  jdbc-kafka-connect-strimzi:3.2.3 /bin/bash
cd /opt/kafka/plugins/
cd /opt/kafka/libs/

# Docker Hub (Container Images Repository)
https://hub.docker.com/repositories

# Tagear a imagem
docker tag jdbc-kafka-connect-strimzi:3.2.3 harlemmuniz/jdbc-kafka-connect-strimzi:3.2.3

# Logar no Docker Hub (digitar usuário e senha)
docker login

# Enviar a imagem para o Docker Registry
docker push harlemmuniz/jdbc-kafka-connect-strimzi:3.2.3

# Remover outras imagens
docker rmi $(docker images --filter "dangling=true" -q --no-trunc) -f
```

### quick build
```sh
# Buildar a imagem mais rápido
docker build . -t jdbc-kafka-connect-strimzi:3.2.0
docker tag jdbc-kafka-connect-strimzi:3.2.0 harlemmuniz/jdbc-kafka-connect-strimzi:3.2.0
docker push harlemmuniz/jdbc-kafka-connect-strimzi:3.2.0
```