# Section 6: Deployment

- [Module contents overview](#module-contents-overview)
- [Large scale deployment challenges](#large-scale-deployment-challenges)
- [Application deployment](#application-deployment)
- [Infrastructure deployment](#infrastructure-deployment)
- [System operations](#system-operations)
- [Modern deployment solutions](#modern-deployment-solutions)
- Application Deployment
  - [Component Deployment](#component-deployment)
  - [Component Deployment Automation](#component-deployment-automation)
  - [Deployment with Virtual Machines](#deployment-with-virtual-machines)
  - [Isolation through virtual machines](#isolation-through-virtual-machines)

---

## Module contents overview

**System Deployment**

- Deployments
  - Application
  - Infrastructure
  - Operations
- Large-Scale Deployments
  - Virtual Machines
  - Docker Containers
  - Kubernetes
- System Upgrades
  - Rolling Upgrades
  - Blue-Green Deployments
  - Recreate Deployments
  - Canary Deployment
 
---

## Large scale deployment challenges

- Application Deployment
- Infrastructure Deployment
- Operations

---

## Application deployment

In Large scale systems we deal with lots of components which need to be replicated for scalability and reliability, that makes the deployment process complex.

- Web Apps
  - Replicas
- Services
  - Microservices & Replicas
- Databases
  - RDBMS, NoSQL
  - Replication & Partitioning
- Message Queues
  - Replication & Partitioning
- Caches
- Directory Servers / LDAP
- Content Storage
- Log File Storage
- Search & Analytics


Deployment is not a one-time activity. It is continuous
- Upgrades
- Bug Fixes

---

## Infrastructure deployment

Application can be deployed on top of this infrastructure

- Compute Infrastructure
  - Compute VMs
    - CPU, RAM, Disks
- Network
  - Routing, Domains
    - Datacenters
  - Internet access
  - Secure access
    - Firewalls, Certificates
- Load Balancers
  - HSL, SLB
- DNS & Discovery Services
- Storage
  - Content, VM / Container
  - Images, Backups, Logs
- Mail Servers
- CDN

We need to provision adequate capacity of infrastructure so that our system can function and scale
when required

Also we need environments for
- Dev
- Test
- Staging
- Prod

---

## System operations

How can we architect our system so that operations run smoothly 

We are looking at engineering solutions which can facilitate these automated operations

![System operations](assets/images/66.png)

---

## Modern deployment solutions

Any deployment process is all about automating the manual steps

- Application Deployment
  - Containers
    - Docker
- Infrastructure Deployment
  - Cloud
    - Google Cloud, AWS
- Operations
  - Kubernetes
- Automation
  - DevOps Tools
    - Vargrant, Ansible, CHEF

---

## Component Deployment

Example: Web Application

- Process
  - Install JVM
  - Install Web Container
    - Configuration
  - Deploy Web App
    - Configuration
- Issues
  - Error Prone
  - Time consuming
  - Repetitive
 
![Component Deployment](assets/images/67.png)

---

## Component Deployment Automation

- Provision a machine with required operating system
- Run a script to install the required software

Benefits
- Reliable
- Easily repeatable
- Less time consuming
- Idempotent
- Declarative
- Remote

Example
```
#!/bin/bash

# Install open jdk 11
apt-get install -y software-properties-common \
&& add-apt-repository ppa:openjdk-r/ppa \
&& apt-get update \
&& apt install -y openjdk-11-jdk

# Install web container Jetty
apt-get install -y jetty9

# Deploy web app: Remote copy war file to jetty war file location
scp user@stagin:/war-files/WebApp.war $USER@localhost:/usr/war/

# Start application: Start Jetty container
java -jar /usr/share/jetty9/start.jar
```

---

## Deployment with Virtual Machines

We can take the component deployment one step further by doing **Virtualization of application components**

We can install Virtual Machine software and we can use it as an image along with the Operation System
- then we take that image to a different machine (running virtual machine software)
- efficient way of repeating the installation

Application had some dependencies on
- OS Version
- exact environment of OS

we have lifted the entire environment and we have completely minimized any chance of incompatibility
- very reliable
- efficiently repeatable
- less time consuming

**Two ways of running a Virtual Machine**
- Using Hypervisor - Type I
  - efficient, typically used in cloud
    - vmware ESXi, Microsoft Hyper-v
    - Bare Metal
    - No underlying OS between hypervisor and physical machine
- Using Hypervisor - Type II
  - Install Virtualization software
    - vmware
    - VirtualBox
  - 2 OSs

![Deployment with Virtual Machines](assets/images/68.png)

---

## Isolation through virtual machines

There is no fixed requirement of any application in terms of Operating System resources like CPU, RAM, disk etc

A good strategy is to buy a large piece of hardware and run multiple applications
- Issue: Hardware is shared across multiple applications
  - e.g. if application 1 runs a batch process it may hog the entire CPU
  - applications 2,3 which are client facing may slow down requests

We can overcome this issue by running Virtual Machines
- fixed quota of resources are allocated to each VM
- No shared resources between applications running virtual machine on the same host machine

![Isolation through virtual machines](assets/images/69.png)

---


