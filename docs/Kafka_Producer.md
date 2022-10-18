### How to Create a Kafka Producer in Java?

There are four steps to create a Java producer:

### 1 - Create a Java Class ProducerDemo.java

### 2 - Create producer properties

Apache Kafka offers various Kafka Properties which are used for creating a producer. To know about each property, visit the official site of Kafka - https://kafka.apache.org/documentation. Navigate to Kafka > Documentation > Configurations > Producer Configs.

The required properties that we must specify are shown below:

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
