# kafka version = 3.2.3 [latest]

# https://www.confluent.io/hub/confluentinc/kafka-connect-jdbc
# https://www.confluent.io/hub/debezium/debezium-connector-sqlserver
# https://github.com/yousufdev/kafka-connect-append-schema
# https://mvnrepository.com/artifact/org.apache.kafka/connect-runtime/2.6.0

# get image from strimzi repository
# https://quay.io/repository/strimzi/kafka
FROM quay.io/strimzi/kafka:latest-kafka-3.2.3

# using root user
USER root:root

# create dirs
RUN mkdir -p /opt/kafka/plugins/kafka-connect-jdbc

# copy jar files
COPY ./jars/kafka-connect-jdbc/ /opt/kafka/plugins/kafka-connect-jdbc/

# copy libs
COPY ./jars/libs/ /opt/kafka/libs/

# user
USER 1001