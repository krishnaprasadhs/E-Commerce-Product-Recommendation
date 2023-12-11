# Product-Recommendation
---
This project demonstrates the implementation of Spark Streaming and Kafka using a real-life e-commerce website product recommendation example. The code allows you to receive the best product recommendations based on a specific item_id.
## Dependencies

- Zookeeper
- Kafka
- Spark: 2.4
- Spark Stream Package: Necessary package it is part of the code.
- Python: 3.7 (for Spark 2.4 version)
## How to run?
All these commands (except for Registry of topics) go in seperate console windows on the terminal.

- **Zookeeper**: zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties <br/>
(Zoopkeeper is the broker that helps coordinate the show)

- **Kafka Server**: kafka-server-start /usr/local/etc/kafka/server.properties <br/>
(Kafka server syncs data flow between Producer and Consumers)

- **Register 1st Topic**: kafka-topics --create --zookeeper localhost:2181 --topic idpushtopic --partitions 1 --replication-factor 1 <br/>
(idpushtopic is the topic to get an Id of product for recommendations. To be run once only.)

- **Register 2nd Topic**: kafka-topics --create --zookeeper localhost:2181 --topic prodRecommSend --partitions 1 --replication-factor 1 <br/>
(prodRecommSend is the topic to which the stream pushes the recommendations. To be run once only.)

- **Producer**: kafka-console-producer --broker-list localhost:9092 --topic idpushtopic <br/>
(Producer to be opened in one window that ultimately pushes the product id to the spark stream)

- **Spark Streaming**: spark-submit --jars spark-streaming-kafka-0-8-assembly_2.11-2.4.7.jar kafka-product-recom.py localhost:2181 idpushtopic <br/>
(Stream helps fetch the Id, run the product recommendation and then acts as producer and pushes to another topic)

- **Consumer**: kafka-console-consumer --bootstrap-server localhost:9092 --topic prodRecommSend --from-beginning <br/>
(Consumer to be opened in one window that ultimately fetches the product list from the spark stream)
## How to test?

- Start Producer in one window and push an item id: 19444 (to test) <br/>

- You'd see things happening on Spark streaming window. <br/>

- Simultaneously you'd get the data in the consumer window <br/>
