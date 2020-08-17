# Table of Contents
[Apache Kafka](#a)  
[Topics, partitions and offsets](#b)  
[Brokers](#c)

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

<a name ="b"/>

## Brokers

* A Kafka cluster is composed of multiple brokers, Brokers means server, its identified by ID (integer)
* Certain topic partitions present in each broker
* Connecting to any broker, you will be connected to the entire cluster
* Good broker number is 3

![](https://imgur.com/UNVy9Dc.png)







