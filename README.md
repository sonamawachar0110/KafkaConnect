# KafkaConnect

This repo is to define generic endpoint where users can connect to particular Kafka Cluster. To start the class diagram for this task will be -

<img width="139" alt="Screen Shot 2023-02-04 at 11 39 34 AM" src="https://user-images.githubusercontent.com/123852517/216786610-09a66248-c665-4c77-b6e8-0dad65531097.png">

## Local Kafka Cluster
The docker compose file creates a local kafka cluster with one zookeeper node and one kafka 
broker. The code for the compose file can be found at [link](https://developer.confluent.io/quickstart/kafka-docker/).  
Access the `Kafkdrop` UI from `localhost:9000`.
### Start kafka cluster
```
docker-compose up
```

### Stop kafka cluster
```
docker-compose down
```

### Create topic
```
docker exec -it broker /bin/bash
$ kafk-topic --bootstrap-server broker:9092 --create --topic demo
```

### List topics
```
kafka-topic --bootstrap-server broker:9092 --list
```