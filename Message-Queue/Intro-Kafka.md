# Kafka

- Events == Notification + State
    - State is normally represented in some structured format, like JSON and Avro
- Data Model for an Event in Kafka
    - Key|Value
        - Keys and values are just sequences of bytes
            - Heavy use o serialization and deserialization
        - Kafka internally is loosely typed
        - Thanks to the key, kafka guarantees the order in the partitions of a topic

- **Topic**
    - Kafka fundamental unit for event organization is called a topic
    - Association: Like a table in a relational database
    - Named container for similar events
        - Systems contaon lots of topics. Usually topics hold different kind of events
        - There may be topics that hold filtered and transformed versions of the same kind of event
        - Ex: Imagene one topic that gets all infos of thermostats in a region
            - It is possible to create another topic that will contain the infos of thermostats that are in a region above a certain temperature (filter operation to populate this topic)
    - A topic is a log (Durable logs of events) - Do not confuse with queue!!
        - Append in the **end** only
        - Can only seek by offset, not indexed 
        - a log is immutable
        - a log is durable -> What does that mean? It means that if some consumer read a message, this action will not destroy it.

- Physical infrastructure standpoint Kafka is composed of a network of machines called brokers
    - An computer, instance, or container running the kafka process
    - Each broker hosts some set of kafka partitions
    - Each broker handles write and read requests
    - Brokers manage replication of particions

- **Consumers**
    - Kafka is able to provide both ordering guarantees and load balancing over a pool of consumer processes
        - This is achieved by assigning the partitions in the topic to the consumers in the consumer group so that each partition is consumed by exactly one consumer in the group
    - [How can Kafka consumers parallelise beyond the number of partitions](https://medium.com/@jhansireddy007/how-can-kafka-consumers-parallelise-beyond-the-number-of-partitions-a0a46ade8a6c)
- Consumer Group

## Kafka Connect
- Data integration system and ecosystem
    - Job of Kafka Connect - "Sometimes you'd like the data that are in those other systems to get into kafka topics, and sometimes you'd like the data in kafka topics to get into those systems"
- Role 1 - Client Application
    - as a client application kafka connect is a server process that runs on hardware independent of the kafka brokers (basically an application runnit outside the cluster)
    - Design to be scalable and fault tolerant
- [Kafka Connect](https://www.youtube.com/watch?v=J6adhl3wEj4&list=PLa7VYi0yPIH0KbnJQcMv5N9iW8HkZHztH&index=11)

## Schema Registry
- New consumers will appear trough out the existenci of a topic. These consumers are goint to need to understand the format of the messages in the topic.
- Tipically, the format of the messagens evolves with the business as well, so changes are inevitable.
- In order to move messagens trough a topic, it is necessary to have a way of agreeing on the schema that the producers and consumers of that topic is able to process ---> Schema registry tries to solve this problem.
- Schema registry looks like an application that is plugable to a kafka cluster.
    - Server process external to kafka brokers.
- Maintains a database of schemas.
    - This database is persisted in a internal kafka topic, and it is cached in the Schema Registry for low latency access.
- Schema regisitry is composed by Consumer/Producer API components
    - Producer API presents incompatible messages from being produced
    - When a producer is configured to use the schema registry, it calls, at produce time, an API at the schema registry REST endpoint, and presents the schema of the new message. If it's the same as the last message produced, then the produce may succeed.
        - If the format is different from the last message, but matchs the compatibility rules defined for the topic,the produce may still succeed.
    - If a consumer reads a message that has an incompatible schema from the version that the consumer code expects, Schema Registry will tell it not to consume the message (this helps to keep runtime failures from happen).
