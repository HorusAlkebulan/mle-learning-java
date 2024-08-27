# Apache Kafka Essential Training: Getting Started

SOURCE: <https://www.linkedin.com/learning/apache-kafka-essential-training-getting-started-22398044>

## Using the Kafka Command Line

1. Please make sure that Docker is already installed in the system,
If not, install from https://www.docker.com/products/docker-desktop

2. If on Windows O/S, open a Powershell window.
If on Mac OS or Linux, open a Terminal window.

3. Navigate to the directory where the exercise files are downloaded.
This directory would contain the kafka-single-node.yml file

4. Ensure Docker Desktop is up and running and execute the following command from this directory

```sh
cd linkedin/apache_kafka_essential_training
docker-compose -f kafka-single-node.yml up -d
```

5. Check if the kafka container are up and running

```sh
docker ps
```

6. To shutdown and remove the setup, execute this command in the same directory

```sh
docker-compose -f kafka-single-node.yml down
```

### Shell into the container

```sh
docker exec -it kafka-broker /bin/bash
```

### Navigate to the Kafka Scripts directory

```sh
cd /opt/bitnami/kafka/bin
```

### Creating new Topics

```sh
kafka-topics.sh \
    --bootstrap-server localhost:29092 \
    --create \
    --topic kafka.learning.tweets \
    --partitions 1 \
    --replication-factor 1

kafka-topics.sh \
    --bootstrap-server localhost:29092 \
    --create \
    --topic kafka.learning.alerts \
    --partitions 1 \
    --replication-factor 1
```

### Listing Topics

```sh
kafka-topics.sh \
    --bootstrap-server localhost:29092 \
    --list
```

### Getting details about a Topic

```sh
kafka-topics.sh \
    --bootstrap-server localhost:29092 \
    --describe
```

### Publishing Messages to Topics

```sh
kafka-console-producer.sh \
    --bootstrap-server localhost:29092 \
    --topic kafka.learning.tweets
```

### Consuming Messages from Topics

```sh
kafka-console-consumer.sh \
    --bootstrap-server localhost:29092 \
    --topic kafka.learning.tweets \
    --from-beginning
```

### Deleting Topics

```sh
kafka-topics.sh \
    --bootstrap-server localhost:29092 \
    --delete \
    --topic kafka.learning.alerts
```

## Kafka Partitions and Groups

### Create a Topic with multiple partitions

```sh
kafka-topics.sh \
    --bootstrap-server localhost:29092 \
    --create \
    --topic kafka.learning.orders \
    --partitions 3 \
    --replication-factor 1
```

### Check topic partitioning

```sh
kafka-topics.sh \
    --bootstrap-server localhost:29092 \
    --topic kafka.learning.orders \
    --describe
```

### Publishing Messages to Topics with keys

```sh
kafka-console-producer.sh \
    --bootstrap-server localhost:29092 \
    --property "parse.key=true" \
    --property "key.separator=:" \
    --topic kafka.learning.orders
```

### Consume messages using a consumer group

```sh
kafka-console-consumer.sh \
    --bootstrap-server localhost:29092 \
    --topic kafka.learning.orders \
    --group test-consumer-group \
    --property print.key=true \
    --property key.separator=" = " \
    --from-beginning
```

### Check current status of offsets

```sh
kafka-consumer-groups.sh \
    --bootstrap-server localhost:29092 \
    --describe \
    --all-groups
```

## Use Case Project

### Creating the Topic

```sh
kafka-topics.sh \
    --bootstrap-server localhost:29092 \
    --create \
    --topic kafka.usecase.students \
    --partitions 2 \
    --replication-factor 1
```

### Describe the Topic

```sh
kafka-topics.sh \
    --bootstrap-server localhost:29092 \
    --topic kafka.usecase.students \
    --describe
```

### Publish to the Topic

```sh
kafka-console-producer.sh \
    --bootstrap-server localhost:29092 \
    --property "parse.key=true" \
    --property "key.separator=:" \
    --topic kafka.usecase.students
```

### Consume Message from the Topic

```sh
kafka-console-consumer.sh \
    --bootstrap-server localhost:29092 \
    --topic kafka.usecase.students \
    --group usecase-consumer-group \
    --property print.key=true \
    --property key.separator=" = " \
    --from-beginning
```
