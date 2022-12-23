# Kafka version = 3.3.1 [latest]

# https://www.confluent.io/hub/confluentinc/kafka-connect-jdbc
# https://www.confluent.io/hub/debezium/debezium-connector-sqlserver
# https://github.com/yousufdev/kafka-connect-append-schema
# https://mvnrepository.com/artifact/org.apache.kafka/connect-runtime/2.6.0

# Pull Kafka image from strimzi repository
# https://quay.io/repository/strimzi/kafka
FROM quay.io/strimzi/kafka:latest-kafka-3.3.1

# using root user
USER root:root

# Create dirs inside Docker volume
RUN mkdir -p /opt/kafka/plugins/kafka-connect-jdbc
RUN mkdir -p /opt/kafka/plugins/kafka-connect-mongodb
# RUN mkdir -p /opt/kafka/plugins/debezium-connector-oracle
# RUN mkdir -p /opt/kafka/plugins/kafka-connect-s3
# RUN mkdir -p /opt/kafka/plugins/kafka-connect-elasticsearch
# RUN mkdir -p /opt/kafka/plugins/kafka-connect-yugabytedb
# RUN mkdir -p /opt/kafka/plugins/debezium-sqlserver-cdc
# RUN mkdir -p /opt/kafka/plugins/debezium-mysql-cdc
# RUN mkdir -p /opt/kafka/plugins/debezium-mongodb-cdc

# Copy jars folders inside Docker Image
COPY ./jars/kafka-connect-jdbc/ /opt/kafka/plugins/kafka-connect-jdbc/
COPY ./jars/kafka-connect-mongodb/ /opt/kafka/plugins/kafka-connect-mongodb/
# COPY ./jars/debezium-connector-oracle/ /opt/kafka/plugins/debezium-connector-oracle/
# COPY ./jars/kafka-connect-s3/ /opt/kafka/plugins/kafka-connect-s3/
# COPY ./jars/kafka-connect-elasticsearch/ /opt/kafka/plugins/kafka-connect-elasticsearch/
# OPY ./jars/kafka-connect-yugabytedb/ /opt/kafka/plugins/kafka-connect-yugabytedb/
# COPY ./jars/debezium-sqlserver-cdc/ /opt/kafka/plugins/debezium-sqlserver-cdc/
# COPY ./jars/debezium-mysql-cdc/ /opt/kafka/plugins/debezium-mysql-cdc/
# COPY ./jars/debezium-mongodb-cdc/ /opt/kafka/plugins/debezium-mongodb-cdc/

# Copy libs inside Docker image
COPY ./jars/libs/ /opt/kafka/libs/


# user
USER 1001