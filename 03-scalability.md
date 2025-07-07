# Section 3: Scalability


- [Performance vs Scalability](#performance-vs-scalability)
- [Vertical & Horizontal Scalability](#vertical--horizontal-scalability)
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


