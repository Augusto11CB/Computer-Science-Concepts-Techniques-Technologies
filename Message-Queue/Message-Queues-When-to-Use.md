# Message Queues When to Use Them
-  message queue is a component for inter-process communication that passes control, content or messages to another component

## Scenarios
- The existence of “timeout errors” due to too many requests at the same time.
- The need a decoupled way to communicate between or within your application (i.e. as the middleman between microservices). 
- Polling a data store too often and you want this data store to be available to answer qualified queries instead
- Need to scale up and down during peak hours
    - When the business and workload grow and the need to scale up the system is obvious, adding more consumers to work on the queues is fast and easy.
- Consumer cannot under any circumstances lose one request
- Processing systems can take their time to process through the messages

> At any time a task is not part of a basic user transaction, and/or the results doesn’t impact a user response, that’s a perfect job for a message queue.

## Use Cases
1. For long-running processes and background jobs
  - web service that handles multiple requests per second and cannot under any circumstances lose one
  - requests are handled through time-consuming processes, but the system cannot afford to be bogged down
  - Examples
    - Images Scaling
    - Sending large/many emails
    - Search engine indexing
    - File scanning
    - Video encoding
    - Delivering notifications
    - PDF processing
    - Calculations


2. As the middleman in between microservices
  - Service that needs to notify another part of the system to start to work on a task or when there are a lot of requests coming in at the same time
  - Examples
    - Order handling
    - Food delivery service
    - Any web service that needs to handle several requests


## References
- [RabbitMQ Use cases: Explaining message queues and when to use them](https://www.cloudamqp.com/blog/rabbitmq-use-cases-explaining-message-queues-and-when-to-use-them.html)
