# Kafka Connectors

### Connectors types:

Source Connector - Bring the event from NoSQL, SQL, and another sources to Kafka topics
Sink Connectors - Get the event in Kafka topics and send to NoSQL, SQL and another sources

JDBC connectors - Query based, to work with databases without CDC and get only INSERT and UPDATE
Debezium connectors - Log based, to with with databases with CDC enabled to get INSERT, UPDATE and DELETE

### SMT - Simple Message Transform #####
It's recommended in cases where you need to do only SIMPLE TRANSFORMATIONS.
Complex transformation it's recommended to use a processing tool as Apache Spark, kSQLDB, Kafka Streams, Flink...

Official documentation - https://docs.confluent.io/5.5.4/connect/transforms/index.html