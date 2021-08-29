# Kafka-Event-Streaming-Big-Picture

> Event streaming is the practice of capturing data in real-time from event sources like databases, sensors, mobile devices, cloud services, and software applications in the form of streams of events; storing these event streams durably for later retrieval; manipulating, processing, and reacting to the event streams in real-time as well as retrospectively; and routing the event streams to different destination technologies as needed. 
> Event streaming thus ensures a continuous flow and interpretation of data.
 
## Kafka Capabilities
- To publish (write) and subscribe to (read) streams of events, including continuous import/export of your data from other systems.
- To store streams of events durably and reliably.
- To process streams of events as they occur or retrospectively.

## How does Kafka Works? 
- Kafka is a distributed system consisting of servers and clients that communicate via a high-performance TCP network protocol. 
- Servers
    - Kafka is run as a cluster of one or more servers that can span multiple datacenters or cloud regions. Some of these servers form the **storage layer, called the brokers**. 
    - Other servers run Kafka Connect to continuously import and export data as event streams to integrate Kafka with your existing systems such as relational databases as well as other Kafka clusters. 

- Clients
  - Clients allow you to write distributed applications and microservices that read, write, and process streams of events in parallel, at scale, and in a fault-tolerant manner.

## Main Concepts and Terminology
- An event records the fact that "something happened" (also called record or message in the documentation)
- When data is written or read to kafka, it is done in the form of events
- An event has a **key, value, timestamp**, and optional **metadata headers**.

```
Event key: "Alice"
Event value: "Made a payment of $200 to Bob"
Event timestamp: "Jun. 25, 2020 at 2:06 p.m."
```

- Producers are those client applications that publish (write) events to Kafka
- Consumers are those that subscribe to (read and process) events.
- **Events** are organized and durably **stored** in **topics** ("a topic is similar to a folder in a filesystem, and the events are the files in that folder")
- Unlike traditional messaging systems, **events are not deleted after consumption**.
    - The existence of an event is done by defining for how long Kafka should retain events
- **Topics are partitioned**, meaning a topic is spread over a number of "buckets" located on different Kafka brokers.
- Any **consumer** of a given topic-partition will always **read** that **partition's events in exactly the same order as they were written**.

## Kafka APIs
- The Admin API to manage and inspect topics, brokers, and other Kafka objects.
- The Producer API to publish (write) a stream of events to one or more Kafka topics.
- The Consumer API to subscribe to (read) one or more topics and to process the stream of events produced to them.
- The Kafka Streams API to implement stream processing applications and microservices. It provides higher-level functions to process event streams, including transformations, stateful operations like aggregations and joins, windowing, processing based on event-time, and more.
- The Kafka Connect API to build and run reusable data import/export connectors that consume (read) or produce (write) streams of events from and to external systems and applications so they can integrate with Kafka. 

![image](https://user-images.githubusercontent.com/17462762/131262185-3a8b68a8-df8f-4348-9036-09ee5f721866.png)
- Image from [kafka.apache.org](https://kafka.apache.org/intro)


