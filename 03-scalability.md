# Section 3: Scalability


- [Performance vs Scalability](#performance-vs-scalability)
- [Vertical & Horizontal Scalability](#vertical--horizontal-scalability)
- [Reverse Proxy](#reverse-proxy)
- [Scalability Principles](#scalability-principles)
- [Modularity](#modularity)
- [Replication](#replication)
  - [Stateful replication in web applications](#stateful-replication-in-web-applications)
  - [Stateless replication in web applications](#stateless-replication-in-web-applications)
  - [Stateless replication of services](#stateless-replication-of-services)
  - [Database replication](#database-replication)
  - [Database replication types](#database-replication-types)
- [Specialized services](#specialized-services)
  - [Specialized services - SOAP / REST](#specialized-services---soap--rest)
  - [Asynchronous services](#asynchronous-services)
- [Asynchronous processing & scalability](#asynchronous-processing--scalability)
- [Caching for scalability](#caching-for-scalability)
- Database partitioning
  - [Vertical partitioning with micro-services](#vertical-partitioning-micro-services)
  - [Database Partitioning](#database-partitioning)
  - [Database Partitioning selection](#database-partitioning-selection)
  - [Routing with database partitioning](#routing-with-database-partitioning)


---

## Overview

- Scalability
  - Vertical & Horizontal Scaling
- Horizontal Scalability
  - Replication
  - Services
  - Caching
  - Asynchronous Process
  - Partitioning
- Load Balancing
  - Load Balancers
  - Service Discovery
  - DNS & Geo Load Balancing
- Micro-Services
  - Architecture
  - Transactions
  - SAGA Pattern
  - NoSQL

---

## Performance vs Scalability

**Fixed Load**

- Performance
  - Low Latency
  - High Throughput
    - Concurrency
      - Single Machine - Multi-Threading
      - Multi Machine - Multi Threading + Multi Processing = Distributed Processing
    - Capacity

**Variable Load**

- Scalability
  - High Throughput
    - Ability of a system to increase its throughput by adding more hardware capacity
  - Both ways - UP and DOWN
 
---


## Vertical & Horizontal Scalability

**Vertical**

- Easier to achieve
- Limited scalability
- Cost raising exponentially
- e.g 4 CPU / 16 GB RAM ➡️ 32 GPU / 256 GB RAM machine

**Horizontal**
- Hard to achieve
- Unlimited scalability
- Cost raising linearly
- e.g. 4 CPU / 16 GB RAM ➡️ 3 x (4 CPU / 16 GB RAM)
- practically immense amount of scalability
- easy to scale down

---

## Reverse proxy

Client having to reach multiple instances of an application, this is only possible if clients can remember the IP addresses of these machines. Those IP addresses are dynamic property and to solve this we use reverse proxy which seats near server side.

- Clint needs to know only about the address of the Reverse Proxy
- Reverse Proxy can also act as a load balancer


**Initial System that we scale**

Web Browser ➡️ Web Application ➡️ Business Application ➡️ Database

---

## Scalability Principles

- Decentralization - Monolith is an anti-pattern for Scalability
  - More workers - Instances, Threads
  - Specialized workers - Services
- Independence
  - Multiple workers are as good as a single worker if they can't work independently
    - They must work concurrently to maximum extent
  - Independence is impeded by
    - Shared resources
    - Shared mutable data

---
  
## Modularity

- Scalable architecture starts with modularity
  - Provides the foundation for breaking an application into more specialized functions / services

Web Browser ➡️ Web Application ➡️ Business Application ➡️ Database

**Business Application**

- API Protocol Layer
- Service Modules
  - User
  - Catalog
  - Order
  - Inventory
- Data Access Layer

Coupled ➡️ Loosely Coupled ➡️ Decoupled

---

## Replication

Web application now has three instances, running exactly the same code
- Stateless / Statefull

Service layer also has 3 instances, running also exactly the same code
- Stateless

Database layer has 2 Databases now, and both have same data
- Stateful

- For handling increasing workloads
  - Stateless
    - Code Replication
    - No data involved in this layer
  - Stateful
    - Code & Data Replication

---

## Stateful replication in web applications

**When low latency is required**

- Sticky sessions / Session affinity
- Sessions occupy memory
- Session clustering for reliability

When first time the request comes, there will be no data in the memory of the web application and we have to go
to the database layer and get the user profile data.

Before giving back the response, we have the opportunity of storing user profile data in the memory of that web application 
instance the request was served

The challenge is that next time the request can go to any web application node ➡️ Solution: Sticky sessions

A cookie exist in the client, that carries the session Id and knows which instance to connect to

**Serious limitations**

- Scalability
  - each session occupies memory
  - maximum number of connections limited by overall memory of the machine
- Reliability
  - if node 1 is no longer alive, where the load balancer should route the request
  - node 3 will have to fetch the information from the database ➡️ high latency, till caches are refreshed
  - changes will be lost in session data ➡️ stale data
    - weblogic provide clustered sessions (copied session data)

In general stateles replication is favoured unless those factors are not considered serious limitations

---

## Stateless replication in web applications

The latency of going to the service may not be that high, but the latency getting data from Database can be very high

- For higher scalability at the expense of higher latency
- Session data can be stored on
  - Client Side in Cookies
  - Server Side in Shared Cache (Memcached / Redis)

preferred architecture, latency cost is only slightly higher

go for stateful architecture when the requirements for latency are extremely critical

---

## Stateless replication of services

**Service Replication**

- Stateless replication - same as web stateless

We can store again in a shared cache data that are frequently read, not frequently modified,
and overcome the latency associated with stateless architecture

When separate instances exist, there is extra complexity because locks cannot be applied. A common technique is to use a lock table in the database.

---

## Database replication

In the context of RDBMS, when the throughput is getting higher we can create a **Read Replica** (Master-Slave configuration). Any change that happens on the primary DB gets automatically propagated and replicated on the Read Replica.

We can also create a **Backup** with replication. If the master goes down, we can promote backup as the master and divert all the traffic load to the new master.

- For higher read scalability
- For high availability


---

## Database replication types

- Master-Slave (Primary-Secondary)
  - Asynchronous - **Read Replica**
    - Low latency writes
    - Eventually Consistent
    - Data Loss
      - In case master goes down, we can promote the secondary as a master but it may result in data loss
    - When we need **high Read Performance**, low latency reads
      - e.g. 5-6 read replicas
  - Synchronous - **Backup**
    - Consistent
    - High latency writes
    - Low write availability
      - if any of both instances goes down, the write operations will have to hold
    - **For backup puproses**
      - e.g. one instance in sync with master which it can replace it in case of failure
  - Common Asynchronous / Synchrous
    - High Read Scalability
    - High Read Availability
    - No Write Conflicts
- Master-Master (No-Master/Peer-To-Peer)
  - Asynchronous - **Multi Geography**
    - Write conflicts
    - High availability
  - Use case
    - High Read Scalability
    - High Read Write Availability
    - Transaction ordering issues


**Master-Slave**

Client can only send read requests to a slave

- Client ➡️ Read + Write ➡️ Master / Primary
- Master / Primary ➡️ Uni-directional Replication ➡️ Slave / Secondary
- Client ➡️ Read ➡️ Slave / Secondary


**Master-Master**

Client can write and read on any of those databases

- Client ➡️ Read + Write ➡️ Master
- Master ⬅️ Bi-directional Replication ➡️ Master
- Client ➡️ Read + Write ➡️ Master

---

## Specialized services

Business application is made of different modules

**Service Modules**
- User
- Catalog
- Order
- Inventory
- Notification

We should be able to add more servers that are dedicated to e.g. host only Inventory module

These issues can be fixed only if we break our monolith application into smaller services

---

## Specialized services - SOAP / REST

![Independent Services](assets/images/06.jpg)

- Partially independent development and deployment
  - e.g. patch only for User Service
- Independent scalability
  - e.g. we can have more number of instances only for a Catalog service
- Independent technology
  - User Service can be a .NET service
  - Catalog a Java Service
  - Order Service in C++

by breaking the monolith application into the business services, we have made some gains in terms of scalability but we have increase the complexity of our system

**RESTful Aggregator / Gateway Service**

- a single point of contact for all of our clients, web / mobile client
- all the background interaction and aggregating the responses will be taken care by gateway service
- we can have an interoperable interface on the gateway
  - we can have gRPC, thrift protocol for internal communication - binary not interoperable, but faster
  - we can have REST protocol for external communication in the gateway


---

## Asynchronous services

We often use message queues to integrate client and server when the interfaces are different and we also use message queues to reliably deliver messages from client to server

- reliable delivery
- integration of different interfaces
- Async services effectively reduces write load from a database

e.g. we want to make order process faster and more reliable ➡️ implement order queue as a buffer

![Asynchronous services](assets/images/07.jpg)

At the order service, we can validate, accept the order and persist it in a message queue

Normally we would process the order but now we are putting it in a message queue (very fast operation)

**Steps involved**

- send a response back to the user when ready
  - that we have accepted the order and we are processing it
  - it is **NOT** the final confirmation that the order has been created
  - it is an acknowledgement that the order has been received
- next step is the order in the messege queue, has to be processed
  - Order processing server
  - it will be notified or pull the orders from the order queue
- order processing server checks the inventory service
- persists the order in the database

We can use asynchronous processing wherever **write operation** is the main operation

---

## Asynchronous processing & scalability

- Async services require infrastructure for average load as opposed to peak load

We want to change the fact that the Database is facing the same load as the Order Service
- The way to do that is asynchronous processing
- the load on our system doesn't remain constant
  - it varies over time
  - peak and down periods
- process requests during low periods of processing

**Example**

- we can scale a db that can process 10000 transactions / seconds to 20000 transactions / second by introducing
  - a message queue
  - an Order Processing Server
- when the overall request rate goes below 10000, during that period the database and order processing server will be able to catch up with the backlog that will be accumulated at Order MQ
- backlog will accumulate during peak periods
- will go away during low periods
- we have distributed the peak load over a period of time
- can work with a lower capacity database
  - but we don't reject any request
  
Order requests ➡️ Order Service PUSH ➡️ **Order MQ** ⬅️ PULL Order Processing ➡️ Order Database

---

## Caching for scalability

- Caching reduces latency and reduces overall read load

**Caching opportunities**

- Data fetched from DB can be cached in Object Cache
- Web application can cache data in Session Cache
- Reverse proxy can cache static data in HTTP Cache
- Browsers or proxies can cache static data in HTTP Cache

Databases are harder to scale because we cannot remove state, that is what it stores

If some of the read load can be served through caches that means we are relieving our database from read load, the additional capacity can be used for write load


![Caching](assets/images/08.png)


The two ways to scale our database, and our entire system
- caching for read load
- asynchronous processing - message queues - for write load

---

## Vertical Partitioning (Micro-Services)

- Micro-Services completely decouples services and databases for higher scalability
- Can no longer do inter service ACID transactions and need to deal with eventual consistency

In order to scale our database we will have to look at what data the database is storing
- Inventory service
- Order service
- Catalog service
- User service

which represent different business domains in our system. 

We can have separate databases for each domain, we have made our system 4 times more scalable

![Vertical Partitioning](assets/images/09.png)

The challenge is if we have common tables, we need to get rid of them, we cannot have common tables, separation of responsibilities

It partitions our database into independent databases and they can take higher write load

---

## Database Partitioning

Database partitioning is used for achieving extreme scalability

### Vertical Partitioning of System

- Catalog
  - DB Node
- Order
  - DB Node
- Inventory
  - DB Node

Splitting database into multiple instances for each domain. This is a vertical partitioning, there is a limit to the extend we can scale.

### Horizontal Partitioning of Database

Splitting of the Order domain into smaller datasets, which we can host into different nodes

**Range Partitioning**

- Order
  - Id 1..100 ➡️ Node 1
  - Id 100..200 ➡️ Node 2
  - Id 200..300 ➡️ Node 3


**Hash Partitioning**

- Order
  - Hash(Id)%N = 1 ➡️ Node 1
  - Hash(Id)%N = 2 ➡️ Node 2
  - Hash(Id)%N = 3 ➡️ Node 3

If we need to rebalance our data (if a node goes down) there is minimum amount of disruption in terms of moving data around


**Common features**

- Partitioning depend on how many nodes we have
  - if we increase / decrease the nodes we will have to change the way we have partitioned the db
  - this is where it's getting complicated
- We **no longer can do ACID transactions**
  - same when they are in different domains
  - we can do only if all records are in the same node
  - in application we have to deal with eventual consistency
  - these are No-SQL databases
  - often RDMS provide also sharding / partitioning
- Makes overall operations more complex because of the added hardware

---

## Database Partitioning selection

Where can we use range and hash partitioning, depends on how we are going to fetch the data

**Range Partitioning**

```
SELECT * FROM Order WHERE id = 150
SELECT * FROM Order WHERE id > 150 AND id < 250
```

- in the second query you have to visit Node 2 and Node 3
- we have to go through a tree like structure in multiple nodes
  - will result to performance penalty

**Hash Partitioning**

```
SELECT * FROM Order WHERE id = 150
```

- we cannot do range queries
- all separate queries will go on separate nodes
- performance of query based of id is must faster than id based query in range partitioning
- hash operation will directly determine the node for the location of key

> Hash partitioning scheme is extremely useful when our access patern of data is predominately on key ids

---

## Routing with database partitioning

**How a database support CRUD operations**

- Client Library (Order Service application)
  - e.g. CouchDB, memcach come with a client library
  - they are cluster-aware, how many nodes in the cluster
  - they apply the hashing algorithm
- Router
  - e.g. MongoDB will provide clients with router component
  - router will determine the node
  - aware of the partitioning scheme
- Go to any node
  - client can contact any node
  - e.g. DynamoDB, CassandraDB
  - that node will take the responsibility of forwarding the request to the correct node

![Routing with Database Partitioning](assets/images/10.png)

---
