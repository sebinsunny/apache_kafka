# Table of Contents
[Apache Kafka](#a)  
[Topics, partitions and offsets](#b)  
[Brokers](#c)  
[Topic Replication](#d)

<a name ="a"/>

## Apache Kafka
It is a open source project created by linkedin, it used to exchange data between many source system and target system. Apache kafka allows to decoupling data streams and systems. 
![](https://imgur.com/CieLc8K.png)

## Apache Kafka: Use Cases
* Messaging System
* Activity Tracking
* Gather metrics from many different locations
* Application Logs gathering
* Stream processing 
* Decoupling of system dependencies

Examples:
* Netflix uses Kafka to apply recommendations in real time, 
* Uber uses Kafka to gather user taxi and trip data in real time to compute and forecast demand and compute surge pricing in real time
* LinkedIn uses Kafka to prevent spam collect user interactions to make better connection recommendations in real time

<a name ="b"/>

## Topics, partitions and offsets

* Topics are similar to table in database
* You can have many topics 
* There is no specific name for topic, you can choose any name
* Topics are split into partition and its ordered
* Each partition have message in it and have a incremental id called offset for each message

![](https://imgur.com/KlfRFBO.png)

Example:

* Let Say u have a fleet of trucks, each truck reports its GPS position to kafka
* Then you have a truck topic ```truck_gps``` that contains the position of all trucks
* Each truck will send a message to Kafka every 20 seconds, each message will contain the truckID and the truck position 

* Offset only have a meaning for a specific partition
* Order is guaranteed only within a partition
* Data is kept only for a limited time
* Once the data is written to a partition, it can't be changed
* Data is assigned randomly to partition unless a key is provided

<a name ="c"/>

## Brokers

* A Kafka cluster is composed of multiple brokers, Brokers means server, its identified by ID (integer)
* Certain topic partitions present in each broker
* Connecting to any broker, you will be connected to the entire cluster
* Good broker number is 3

![](https://imgur.com/UNVy9Dc.png)

<a name ="d"/>

## Topic Replication 

* helps to access the data if one brokers fails, a replication factor is assigned with Topic, I usually between 2 and 3
* if one broker is down and another broker can serve the data
* at a time one broker can be leader for a given partition
* The other broker synchronize the data
* if the down broker was up then it automatically transfer the leadership to the broker

![](https://imgur.com/BnOszGn.png)

## Starting apache kafka

* first need to start the zookeeper server by 
```sh
bin/zookeeper-server-start.sh config/zookeeper.properties
```
* second step is to start apache kafka by 
```sh
bin/kafka-server-start.sh config/server.properties
```
* to create topic need to specify the topic name and the bootstrap server

```sh
bin/kafka-topics.sh --create --bootstrap-server 127.0.0.1:9092 --topic cities
```
* to list the topics in the zookeeper
```sh
bin/kafka-topics.sh --list --zookeeper 127.0.0.1:2181
```
* to describe the topics in zookeeper by passing the topics name
```sh
bin/kafka-topics.sh --list --zookeeper 127.0.0.1:2181
```
* to start producer u need to specify the broker list which is the kafka broker by , then followed by topic name

```sh
bin/kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic cities
```

* consumer console
```sh
 bin/kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic cities
```
* Run a debezium Kafka connector
```sh
export CLASSPATH=/test/kafka-3.0.0-src/connect/debezium-connector-postgres/*
bin/connect-distributed.sh config/connect-distributed.properties
```


