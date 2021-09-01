- SQL
    - It is very restrictive
        - Data-strcture predefined
        - Requires significant upfront preparation
        - Change data structure can be a chanlenge
    - ACID properties - Atomicity, Consistency, Isolation & Durability

- NoSQL
    - have dynamic schemas for unstructured data
        - create documents without having to first define their structure
    - Read/Write throughput is very high

- SQL databases usually deal with structured data that is organized in the form of tables. On the other hand, NoSQL databases, along with support for structured data, offer the convenience of storing unstructured, semi-structured, and polymorphic data as well.

- Database Scaling
    - Horizontal scaling means that you scale by adding more machines into your pool of resources whereas
    - Vertical scaling means that you scale by adding more power (CPU, RAM) to an existing machine.
    - Scalability refers to how a database technology adapts to an ever-increasing amount of data without sacrificing performance.
    - SQL databases tend to be vertically scalable, in the sense that additional load can be handled by using more efficient and newer hardware (CPUs, RAM and SSD). 
    -  NoSQL databases tend to be more horizontally scalable (they can automatically handle more traffic by distributing it among more servers in the database cluster)

- NoSQL Horizontal Scaling > SQL Horzontal Scaling

- RDBMS ACID vs NOSQL BASE + CAP theorem
- ACID: Atomicity, Consistency, Isolation, Durability
    - Atomicity: It ensures all-or-none rule for database modifications.
    - Consistency: Data values are consistent across the database.
    - Isolation: Two transactions are said to be independent of one another.
    - Durability: Data is not lost even at the time of server failure.
- BASE: Basically Available, Soft State, Eventually Consistent
    - A BASE system gives up on consistency.
    - **Basically available** indicates that the system does guarantee availability, in terms of the CAP theorem.
    - **Soft state** indicates that the state of the system may change over time, even without input. This is because of the eventual consistency model.
    - **Eventual consistency** indicates that the system will become consistent over time, given that the system doesn't receive input during that time.
- CAP: Consistency, Availability and Partition tolerance


- When Use No SQL
    - When ACID support is not needed
    - When Traditional RDBMS model is not enough
    - Data which need a flexible schema
    - Constraints and validations logic not required to be implemented in database
    - Logging data from distributed sources
    - It should be used to store temporary data like shopping carts, wish list and session data

- CAP Theorem
    - The CAP theorem saysthat a distributed system can deliver only two of three desired characteristics: consistency, availability, and partition tolerance (the ‘C,’ ‘A’ and ‘P’ in CAP).

    - A distributed system is a network that stores data on more than one node (physical or virtual machines) at the same time. Because all cloud applications are distributed systems, it’s essential to understand the CAP theorem when designing a cloud app.

    - Consistency - "Consistency means that all clients see the same data at the same time, no matter which node they connect to. For this to happen, whenever data is written to one node, it must be instantly forwarded or replicated to all the other nodes in the system before the write is deemed ‘successful.’"

    - Availability - "Availability means that that any client making a request for data gets a response, even if one or more nodes are down. Another way to state this—all working nodes in the distributed system return a valid response for any request, without exception."

    - Partition Tolerance - "A partition is a communications break within a distributed system—a lost or temporarily delayed connection between two nodes. Partition tolerance means that the cluster must continue to work despite any number of communication breakdowns between nodes in the system."

## Reference
- [Cap-Theorem](https://www.ibm.com/cloud/learn/cap-theorem)
- [A Beginner's Reference to SQL vs. NoSQL](https://algodaily.com/lessons/a-beginners-reference-to-sql-vs-nosql)
- [Explanation of BASE terminology](https://stackoverflow.com/questions/3342497/explanation-of-base-terminology)
