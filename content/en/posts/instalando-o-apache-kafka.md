---
  card_desc: "Hey folks! Today I'd like to share a bit about Apache Kafka. I've been working with Kafka to sync data across multiple databases and"
  card_image: http://diegofranca.dev/wp-content/uploads/2024/05/apache_kafka_logo-1200x547-1.png
  card_title: Installing Apache Kafka
  og_desc: "Hey folks! Today I'd like to share a bit about Apache Kafka. I've been working with Kafka to sync data across multiple databases and"
  og_image: http://diegofranca.dev/wp-content/uploads/2024/05/apache_kafka_logo-1200x547-1.png
  og_image_alt:
  og_title: Installing Apache Kafka
_edit_last: "1"
_oembed_c489d0b81b680c45bb060213d62e56bb: '{{unknown}}'
_thumbnail_id: "552"
author: diego.tg.franca@gmail.com
  - uncategorized
  alt: apache_kafka_logo-1200x547
  image: /wp-content/uploads/2024/05/apache_kafka_logo-1200x547-1.png
date: "2024-05-25T15:38:52+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
  page-builder: {}
    builder_active: false
    json: '[]'
guid: https://diegofranca.dev/?p=543
parent_post_id: null
post_id: "543"
summary: '{{ double-space-with-newline }}Hey folks! Today I'd like to share a bit about Apache Kafka. I've been working with Kafka to sync data across multiple databases and thought it would be interesting to share some of what I've been learning. Also, this article will be a place I can easily come back to whenever I have a question in the future.
  - kafka
title: Installing Apache Kafka
  - /2024/05/25/instalando-o-apache-kafka/
---

Hey folks! Today I'd like to share a bit about Apache Kafka. I've been working with Kafka to sync data across multiple databases and thought it would be interesting to share some of what I've been learning. Also, this article will be a place I can easily come back to whenever I have a question in the future.

# What is Apache Kafka

Apache Kafka is an open-source platform for streaming data in a continuous flow. It's a high-performance, real-time messaging system. In recent years, Apache Kafka has become very popular due to the growing adoption of microservices.

## **Nomenclature**

Before we begin the installation, let me explain some terms that will appear throughout this article:

- **Producer**: Allows applications to publish (transmit) content.
- **Consumer**: Allows applications to subscribe to/consume topics and stream processor outputs.
- **Broker**: The concept of a broker in the Kafka platform is basically Kafka itself — it's what manages topics, defines how messages are stored and the logs.
- **Topic**: A topic is a way to label or categorize a message.
- **Partition**: It's the unit of parallelism for Kafka producers and consumers. The number of partitions is defined when a topic is created and can be increased at any time afterward, but never decreased.

# 1\. Installing Apache Kafka

The requirement to run Kafka is to have the JDK installed on the machine. Now, let's download it by clicking the link below:

[https://www.apache.org/dyn/closer.cgi?path=/kafka/3.4.0/kafka_2.13-3.4.0.tgz](https://www.apache.org/dyn/closer.cgi?path=/kafka/3.4.0/kafka_2.13-3.4.0.tgz)

Extract the file:

```
tar -xzf kafka_2.13-3.4.0.tgz
```

Rename it:

```
mv kafka_2.13-3.4.0 kafka
```

Enter the directory:

```
cd kafka
```

## 1.1 **Configuring the Broker**

Let's open the file `kafka/config/server.properties` and edit the following parameters:

- `broker.id=1` (we add a unique integer, which is the broker's identifier).
- `listeners=PLAINTEXT://:9092` → in listeners, uncomment and add the port on which the broker will be accessed.
- `log.dirs=c:/kafka/kafka-log`: we can add the path where the logs will be stored.

## 1.2 Starting Zookeeper

Let's start Zookeeper first:

```
bin/kafka-topics/zookeeper-server-start.bat config/zookeeper.properties

```

After Zookeeper is up, let's start the broker:

```
bin/kafka-topics/kafka-server-start.sh config/server.properties
```

### 1.3 Creating a topic for testing:

With the servers online, let's create the topics:

```
bin/kafka-topics.sh --create --topic test-topic-replicated --bootstrap-server localhost:9092 --replication-factor 3 --partitions 3

```

### 1.4 Creating a consumer to test

```
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test-topic-replicated

```

# 2\. Configuring KAFKA for remote access

To allow external systems to connect to Kafka, we need to add the following configuration to the brokers. First, open the configuration file for your broker:

```
kafka/config/server.properties

```

Once the file is open, look for the line that looks like this:

```
advertised.listeners=PLAINTEXT://your.host.name:9092
```

After uncommenting it, add the IP address through which you have external access. Once you've done that, just restart ZooKeeper and the broker to allow remote connections to Kafka.

{{< adsense >}}
