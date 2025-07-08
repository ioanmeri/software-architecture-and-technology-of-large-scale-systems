# Section 3: Scalability


- [Performance vs Scalability](#performance-vs-scalability)
- [Vertical & Horizontal Scalability](#vertical--horizontal-scalability)
- [Reverse Proxy](#reverse-proxy)
- [Scalability Principles](#scalability-principles)
- [Modularity](#modularity)


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

