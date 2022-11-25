# Kafka-Stearming
This repository contains details of Kafka streaming and its core component
<h2>Kafka :</h2>
<p>Kafka is event streaming platform which needed especially when there are multiple event sources and destination.</p>
<p>Event Streaming : whenever something is happen we say event has occurs,consequentely it generates data. Event streaming consists in capturing event data as soon the event occurs, storing and processing these events.</p>
  
https://medium.com/@TimvanBaarsen/apache-kafka-cli-commands-cheat-sheet-a6f06eac01b


mportant Commands:

To start the Zookeeper:

    bin/zookeeper-server-start.sh config/zookeeper.properties (This will run in foreground)

    bin/zookeeper-server-start.sh -daemon config/zookeeper.properties (This will run in background)

To validate Zookeeper is the start or not:

    echo stat | nc localhost 2181

To Stop the zookeeper:

    bin/zookeeper-server-stop.sh config/zookeeper.properties

To start the Kafka server:

    bin/kafka-server-start.sh config/server.properties (This will run in foreground)

    bin/kafka-server-start.sh -daemon config/server.properties (This will run in background)

To validate kafka server is started or not:

    echo dump | nc localhost 2181 | grep broker

To stop the kafka server:

    bin/kafka-server-stop.sh config/server.properties

To create the Topic:

    bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic TopicName --partitions 1 replication-factor 1

To check a number of Topics presents:

    bin/kafka-topics.sh --bootstrap-server localhost:9092 --list

To check description/properties of any topic (like partition,replication,leader):

    bin/kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic TopicName

To change the number of partitions after creating the topic:

    bin/kafka-topics.sh --bootstrap-server localhost:9092 --alter --topic TopicName --partitions 2

To delete the topic:

    bin/kafka-topics.sh --bootstrap-server localhost:9092 --delete --topic TopicName

To create the Producer:

    bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic TopicName

To create the Consumer:

    bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic TopicName

    bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic TopicName --from-beginning (This will fetch all msg from startig )

To check kafka consumer Group:

    bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --list

To check description/properties of consumer group ( like current offset, log-end offset ):

    bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --describe --group console-consumer-83576

To create own consumer group:

    bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic TopicName -group myConsumerGroup

To delete consumer group:

    bin/kafka-consumer-groups.sh --bootstrap-server 199.199.50.105:9092,199.199.50.59:9092 --delete --group myConsumerGroup

To change the replication factor:

Step 1: Create the JSON file with the name suggestated.json with the below content as per requirements.

{"version":1,"partitions":[{"topic":"TBData","partition":0,"replicas":[1,2,3]}]}

You can change the replicas as per your requirement.

Step 2: Run the below command,

    bin/kafka-reassign-partitions.sh --bootstrap-server localhost:9092 --reassignment-json-file suggestated.json –execute

 
 To check kafka version:

    bin/kafka-topics.sh --version

   


