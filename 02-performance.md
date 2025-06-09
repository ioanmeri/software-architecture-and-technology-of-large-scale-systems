# Section 2: Performance

## System Performance

- Understanding Performance
  - Problems
  - Measurement
  - Principles
- Latency
  - CPU
  - Network
  - Disk
- Concurrency
  - Locking
    - Pessimistic
    - Optimistic
  - Coherence
- Caching
  - Static Data
  - Dynamic Data


**Sample System**

![Sample System](assets/images/01.png)

---

## What is Performance

- Measure of how fast or responsive a system is under
    - A given workload
        - Backend data
        - Request volume
    - A given hardware
        - Kind
        - Capacity

**Goals** 

1. As we increase the workload, performance should stay stable, it should not severely degrate
2. If we increase the hardware capacity, system performance shoould improve

### Performance Problems

How to spot a Performance Problem? How does it look like?

> Every performance problem is the result of some queue building somewhere

> Network socket queue, DB IO queue, OS run queue etc

<b>Reasons for queue build-up</b>
- Inefficient slow processing
- Serial resource access
- Limited resource capacity


Goal: To identify where this build up is happening

---



