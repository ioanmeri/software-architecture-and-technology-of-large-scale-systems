# Section 4: Reliability

- [Module contents overview](#module-contents-overview)
- [Failures in large scale distributed systems](#failures-in-large-scale-distributed-systems)
- [Partial system failures](#partial-system-failures)
- Reliability engineering topics
  - [Reliability](#reliability)
  - [Availability](#availability)

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
