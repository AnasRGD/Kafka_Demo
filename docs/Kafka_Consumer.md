### How to Create a Kafka Producer in Java?

These are the steps to create a Kafka consumer:

### 1 - Create a Java Class ConsumerDemo.java

### 2 - Create the consumer properties

Similar to the producer properties, Apache Kafka offers various different properties for creating a consumer as well. To know about each consumer property, visit https://kafka.apache.org/documentation/#consumerconfigs Apache Kafka > Documentation > Configuration > Consumer Configs.

Here, I will list the required properties of a consumer:

  - **key.deserializer**: It is a Deserializer class for the key, which is used to implement the org.apache.kafka.common.serialization.Deserializer interface.

  - **value.deserializer**: A Deserializer class for value which implements the org.apache.kafka.common.serialization.Deserializer interface.

  - **bootstrap.servers**: It is a list of host and port pairs that are used to establish an initial connection with the Kafka cluster. It does not contain a full set of servers that a client requires. Only the servers which are required for bootstrapping are required.

  - **group.id**: It is a unique string that identifies the consumer of a consumer group.

  - **auto.offset.reset**: This property is required when no initial offset is present or if the current offset does not exist anymore on the server. There are the following values used to reset the offset values:

      - **earliest**: This offset variable automatically reset the value to its earliest offset.

      - **latest**: This offset variable reset the offset value to its latest offset.

      - **none**: If no previous offset is found for the previous group, it throws an exception to the consumer.

### 3 - Create a consumer

Create an object of KafkaConsumer leveraging our properties, as shown below:

        // create consumer
        KafkaConsumer<String, String> consumer = new KafkaConsumer<>(properties);

### 4 - Subscribe the consumer to a specific topic

To read the messages from a topic, we need to connect the consumer to the specified topic. Here, we use Arrays.asList(),as it allows our consumer to subscribe to multiple topics.

Below code shows the implementation of subscription of the consumer to one topic:

        // subscribe consumer to our topic(s)
        consumer.subscribe(Arrays.asList(topic));

### 5 - Create a Poll loop to receive data

The consumer reads data from Kafka through the polling method. The poll method returns the data that hasn't been fetched yet by the consumer subscribed to the partitions. The duration of the poll call for example .poll(Duration.ofMillis(100)) is the amount of time to block on this call before returning an empty list in case no data was returned (also called long polling).

        // poll for new data
        while(true){
            ConsumerRecords<String, String> records =
                    consumer.poll(Duration.ofMillis(100));

            for (ConsumerRecord<String, String> record : records){
                log.info("Key: " + record.key() + ", Value: " + record.value());
                log.info("Partition: " + record.partition() + ", Offset:" + record.offset());
            }
        }
