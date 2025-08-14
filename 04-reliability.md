# Section 4: Reliability

- [Module contents overview](#module-contents-overview)
- [Failures in large scale distributed systems](#failures-in-large-scale-distributed-systems)

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
