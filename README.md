# KafkaConnect

This repo is to define generic endpoint where users can connect to particular Kafka Cluster.

## Kafka Connect Cluster
The docker compose file creates a local Kafka Connect cluster that runs on top of Kafka cluster in containers. The
code was copied and modified from Confluent's repository ([link](https://github.com/confluentinc/demo-scene/blob/master/csv-to-kafka/docker-compose.yml)).
The result of the ingestion process can be seen on  
 
### Start the kafka Connect cluster
```
docker-compose -f load-csv-kafka.yml up
```

### Create connector
```
curl -i -X PUT -H "Accept:application/json" \
    -H  "Content-Type:application/json" http://localhost:8083/connectors/source-csv-spooldir-00/config \
    -d '{
        "connector.class": "com.github.jcustenborder.kafka.connect.spooldir.SpoolDirCsvSourceConnector",
        "topic": "orders_spooldir_00",
        "input.path": "/csv/unprocessed",
        "finished.path": "/csv/processed",
        "error.path": "/csv/error",
        "input.file.pattern": ".*\\.csv",
        "schema.generation.enabled":"true",
        "csv.first.row.as.header":"true"
        }'
```

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

### Note
```
If Kafka Connect is returning status as "Unhealthy" , increase the memory to 8GB in Docker Desktop
```