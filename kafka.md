## Basic Kafka commands

### Test Zookeeper and Kafka broker registration to the Zookeeper server.
zookeeper-shell.bat localhost:2181 ls /brokers/ids

### Create a new Kafka topic
kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic topic1

### Describe a Kafka Topic
kafka-topics.bat --describe --zookeeper localhost:2181 --topic topic1

### Show the available topics
kafka-topics.bat --list --zookeeper localhost:2181  

### Start a console producer and send some messages 
kafka-console-producer.bat --broker-list localhost:9092 --topic topic1

### Publish message from a file
kafka-console-producer --broker-list localhost:9092 --topic topic1 < C:\Work\camel\test\input.txt

### Sending msg with both keys and values, set the --parse.key property to true & --key.separator property to a separator (i.e. comma, semicolon, colon etc.) 
kafka-console-producer --broker-list localhost:9092 --topic topic1 --property "parse.key=true" --property "key.separator=:"

### Read messages from the beginning
kafka-console-consumer --bootstrap-server localhost:9092 --topic topic1 --from-beginning
kafka-console-consumer --bootstrap-server localhost:9092 --topic topic1

### Read message with key:value
kafka-console-consumer --bootstrap-server localhost:9092 --from-beginning --topic topic1 --property print.key=true

### Delete Topic
kafka-run-class.bat kafka.admin.TopicCommand --delete --topic topic1 --zookeeper localhost:2181

### Performance producer
kafka-producer-perf-test --topic topic2 --num-records 1000000 --throughput -1 --producer-props bootstrap.servers=localhost:9092 batch.size=1000 acks=1 linger.ms=100000 buffer.memory=4294967296 compression.type=text request.timeout.ms=300000 --record-size 1000

### Performance consumer
kafka-consumer-perf-test --topic topic2 --broker-list localhost:2181 --messages 1000 --timeout 1000
kafka-consumer-perf-test --topic topic2 --zookeeper localhost:2181 --messages 150 --threads 1
