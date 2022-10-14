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

There are four steps to create a Java producer:

 ### 1 - Create a Java Class ProducerDemo.java
 
 ### 2 - Create producer properties

Apache Kafka offers various Kafka Properties which are used for creating a producer. To know about each property, visit the official site of Kafka - https://kafka.apache.org/documentation. Navigate to Kafka > Documentation > Configurations > Producer Configs.

he required properties that we must specify are shown below:

- **bootstrap.servers**: It is a list of the port pairs which are used for establishing an initial connection to the Kafka cluster. We use the bootstrap servers for making an initial connection to the cluster. This server is present in the host:port, host:port,... form.

- **key.serializer**: It is a type of Serializer class of the key that is used to implement the org.apache.kafka.common.serialization.Serializer interface.

- **value.serializer**: It is a type of Serializer class which implements the org.apache.kafka.common.serialization.Serializer interface.




  ### 3 - Create the producer
 
To create a Kafka producer, we just need to create an object of KafkaProducer
        KafkaProducer<String, String> producer = new KafkaProducer<>(properties);
  
  
  
  ### 4 - Create a producer record
 
 In order to send the data to Kafka, we need to create a ProducerRecord. Here, the producer specifies the topic name as well as the message value which is to be delivered to Kafka. The key is assumed to be null in this instance.

A ProducerRecord can be created as:
        ProducerRecord<String, String> producerRecord =
                new ProducerRecord<>("topic_name", "hello world");
          
          
          
          
                
  ### 5 - Send the data

Now, we are ready to send the data to Kafka. The producer just needs to invoke the object of the ProducerRecord as:

        // send data - asynchronous
        producer.send(producerRecord);

        // flush data - synchronous
        producer.flush();
        
        // flush and close producer
        producer.close();
        
  The data produced by a producer is asynchronous. Therefore, two additional functions, i.e., flush() and close() are required to ensure the producer is shut down after the message is sent to Kafka.

The flush() will force all the data that was in .send() to be produced and close() stops the producer. If these functions are not executed, the data will never be sent to Kafka as the main Java thread will exit before the data are flushed.
