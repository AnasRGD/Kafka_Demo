# Kafka_Demo

In this repo, I will use Java programming language to :
  - programmatically read data from standard input and publish it to Kafka.
  - pull event data from one or more Kafka topics known as Kafka Consumers.

## Kafka Producers

Applications that send data into topics are known as Kafka producers. Applications typically integrate a Kafka client library to write to Apache Kafka.
A Kafka producer sends messages to a topic, and messages are distributed to partitions according to a mechanism such as key hashing.
For a message to be successfully written into a Kafka topic, a producer must specify a level of acknowledgment (acks).

![image](https://user-images.githubusercontent.com/68516240/195882706-7b93e1c7-0fa6-4e55-9992-80099e912c2a.png)

### Kafka Message Anatomy

Kafka messages are created by the producer. A Kafka message consists of the following elements:

![image](https://user-images.githubusercontent.com/68516240/195883070-3215f41c-ee6e-449a-a62a-86d1ce39e649.png)

- **Key** : Key is optional in the Kafka message and it can be null. A key may be a string, number, or any object and then the key is serialized into binary format.

- **Value** : The value represents the content of the message and can also be null. The value format is arbitrary and is then also serialized into binary format.

- **Compression Type** : Kafka messages may be compressed. The compression type can be specified as part of the message. Options are none, gzip, lz4, snappy, and zstd

- **Headers** : There can be a list of optional Kafka message headers in the form of key-value pairs. It is common to add headers to specify metadata about the message, especially for tracing.

- **Partition + Offset** : Once a message is sent into a Kafka topic, it receives a partition number and an offset id. The combination of topic+partition+offset uniquely identifies the message

- **Timestamp** : A timestamp is added either by the user or the system in the message.






### Creating a Kafka Java Project using Maven (pom.xml)


First, I will define the Kafka Dependencies by creating a <dependencies>...</dependencies> block within which I will define a dependency for Kafka client and another ones logging. This will enable us to print diagnostic logs while our application runs. Our dependency block is as shown below : 

    <dependencies>
        <!-- https://mvnrepository.com/artifact/org.apache.kafka/kafka-clients -->
        <dependency>
            <groupId>org.apache.kafka</groupId>
            <artifactId>kafka-clients</artifactId>
            <version>3.0.0</version>
        </dependency>

        <!-- https://mvnrepository.com/artifact/org.slf4j/slf4j-api -->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.7.32</version>
        </dependency>

        <!-- https://mvnrepository.com/artifact/org.slf4j/slf4j-simple -->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-simple</artifactId>
            <version>1.7.32</version>
        </dependency>
    </dependencies>


### How to Create a Kafka Producer in Java?

Tutorial available at : https://github.com/AnasRGD/Kafka_Demo/blob/master/docs/Kafka_Producer.md


### How to Create a Kafka Consumer in Java?

Kindly check documentation : https://github.com/AnasRGD/Kafka_Demo/blob/master/docs/Kafka_Consumer.md
