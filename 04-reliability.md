# Section 4: Reliability

- [Module contents overview](#module-contents-overview)
- [Failures in large scale distributed systems](#failures-in-large-scale-distributed-systems)
- [Partial system failures](#partial-system-failures)
- Reliability engineering topics
  - [Reliability](#reliability)
  - [Availability](#availability)
  - [High Availability](#high-availability)
  - [Fault Tolerance](#fault-tolerance)
- Designing Fault Tolerance
  - [Fault Tolerant design](#fault-tolerant-design)
  - [Redundancy](#redundancy)
  - [Types of redundancy](#types-of-redundancy)

---

## Module contents overview

**System Reliability**

- Reliability
  - Availability, Reliability
  - Fault Tolerance
  - Partial Failurs
- Designing Fault Tolerance
  - Redundancy
    - Hot, Warm, Cold
  - Fault Detection
    - Health Checks, Monitoring
  - Recovery
    - Stateless, Stateful
- System Stability
  - Timeouts
  - Circuit Breakers
  - Fail Fast, Shed Load

---

## Failures in large scale distributed systems

To make systems horizontally scalable, we need to make them distributed

- Large scale systems are generally distributed systems
  - Large number of components
  - Large number of component instances
- Failures can be
  - Partial
  - Independent
    - e.g. a service component instance goes down
    - requests will be diverted to the other instances
  - Single point of failures
    - e.g. database goes down, it will affect the entire system (except static cached pages)
- Increased chance of partial failures
- Partial failures can lead to complete system failures
  - e.g load balancer fails, no requests will be served by the system

We will look at what kind of failures can happen to the system, how they can impact the system, what are the different architecture principles that we can 
use to make the system more resilient to these failures

---

## Partial system failures

- Network failure - LAN, WAN, Load Balancer
- Machine Failure - CPU, Disk, Memory
- Software Failure - Process
- Disaster - Datacenter
- Operations
  - Deployment Failure
  - Configuration Failure
  - Load Induced Failure
  - External Service Failure

After a point, its much more economical to recover from a failure instead of preventing it altogether

- **No matter how hard we try**
  - **Hardware and Networks will fail**
  - **A changing Software will fail**
  - **Disasters will happen**

---

## Reliability

- A system is said to be reliable if it can continue to function correctly and remain available for operations even in the presence of partial failures
- It is measured as the probability of a system working correctly in a given time interval

---

## Availability

Availability extends the reliability property, refers to the unavailable time

- It is the probability of a system working correctly at any given time and being available for operations
  - Time based availability = uptime / (uptime + downtime)
  - Request based availability = successful requests / total requests
- There can be downtime but the system is expected to recover from the same in a quick time

---

## High Availability

- Availability requirements should come from the impact of availability on a business
- Beyond business, availability is at the cost of
  - New features
  - Operational costs
- The system should use downtimes permitted by SLA / SLO for rollout of new features
  - New feature rollouts invariably cause disruptions


**Availability Requirements**

| Availability | Max Disruption (per year) | Application Categories |
| -----------  | ------------------------- | ---------------------- |
| 99% | 3 days 15 hours | Batch processing, data extraction, transfer, and load jobs |
| 99.9% | 8 hours 45 minutes | Internal tools like knowledge management, project tracking |
| 99.95% | 4 hours 22 minutes | Online commerce, point of sale |
| 99.99% | 52 minutes | Video delivery, broadcast systems |
| 99.999% | 5 minutes | ATM transactions, telecommunications systems |

---


## Fault Tolerance

- Fault Tolerance is a technique to improve Availability and / or Reliability of a system
- It is commonly referred to as an ability of a system to automatically
  - Detect partial failures
  - Handle partial failures
  - Recover from partial failures
- Serviceability
  - The ease with which a system can be serviced in the event of a failure also determines the availabilit of a system

 ---

## Fault Tolerant design

The are three steps in designing a fault tolerant system:

1. Redundancy
2. Fault Detection
3. Recovery

---

## Redundancy

- Replication / Duplication of critical components or functions of a system in order to increase its reliability
- A secondary capacity is kept ready as a backup, over and above the primary capacity, in case the primary is not available

**Example**

It a three tier design: web serverice, business application, database

The single instance of business application goes down and makes the entire application unavailable

We will need to provision redundancy in case the primary instance goes down

---

## Types of redundancy

- Active Redundancy - Hot Spare
  - All nodes do the processing
  - Ideal for providing highest availability
- Passive Redundancy - Warm Spare
  - Only actives nodes do the processing
  - Ideal for quick recovery
  - Redundancy is not in operation 
- Cold Redundancy - Spare (Backup)
  - Spare nodes are brought up only on a failover
  - It is not a high availability option
  - Only when primary instance goes down, we make arrangements to provision secondary capacity
    - There is a significant time delay till second capacity take over
    - low cost option

---
