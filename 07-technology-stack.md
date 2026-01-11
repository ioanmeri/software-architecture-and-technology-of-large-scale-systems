# Section 7: Technology Stack

- [Module contents overview](#module-contents-overview)
- [Reference system](#reference-system)
- [Web applications](#web-applications)
  - [Solutions for web applications](#solutions-for-web-applications)
  - [Apache web server](#apache-web-server)
  - [Apache webServer architecture](#apache-webserver-architecture)
  - [Apache webserver scalability](#apache-webserver-scalability)

---

## Module contents overview

- Platforms for
  - Web Apps
  - Services
  - Datastores
  - Analytics
- Platform Functionality
- Platform Architecture
  - Performance
  - Scalability
  - Reliability
- Platform Use-Cases
- Platform Alternatives
  - Comparison
- Architecting Solution
  - End-to-End

---

## Reference system

![Reference system](assets/images/90.png)

Layers of the system
- Web
- Services
- Database
- Analytics

represents a complete system

We are interested in the **functionality** of the platform that will be used

Also, we are interested in the **non-functional** aspects of the product
- Scale
- Resiliant
- Reliable
- Secure
- Perform

---

## Web applications

The frontend part of the application, we are concert how to
- build the server side of the system

The most important challenges are
- they receive the highest amount of load
- they are connected to clients which are located in long distances
- the communication must be secure

as we go down the system the load decreases progressively

We look at how efficiently it can serve the content and how much load it can handle.

![Web applications](assets/images/91.png)

---

## Solutions for web applications

- Static Content
  - Apache Web Server
  - Nginx Web Server
  - Cloud storage
- Dynamic Content
  - Web Server - Apache HTTPD, NodeJS
  - Java Web Containers - Tomcat, Jetty, Spring-Boot
- Content Caching
  - Nginx
- Content Distribution
  - CDN

---

## Apache web server

Apache Webserver can

- Store Static Content
  - HTML / CSS / JS files
  - Images files
  - Documents
- Generate Dynamic Content
  - Get data & generate pages dynamically
  - PHP, Python, Perl
  - No JSP / Servlets
- Act as a Reverse Proxy LB
  - Not great
  - Single point of contact with IP and will proxy all requests to backend web application

IO from disk can be slow, when fetching first time the file Apache will store the file in RAM 
- 64 GB RAM minimum depending on static content
- Heavily overloaded CPU and RAM for dynamic content

![Apache Webserver](assets/images/92.PNG)

---

## Apache webServer architecture

- Based on Request-Response Model
- Clients connect using HTTP protocol
- Apache can provide persistent connections
  - each connection will occupy some memory
  - each connection will be allocated a thread from a thread pool
  - thread may access CPU, memory or network

When fetching dynamic pages the thread will 
- use a lot of CPU to process the page
- may use network to fetch data from database or service

A thread either using CPU or IO 

When processing a lot of pages Apache will run out of memory or CPU.

![Apache Webserver](assets/images/92.png)

---

## Apache webserver scalability

Depends on how Apache it is used
- Apache as Webserver
  - For serving static / dynamic content
  - We can add more nodes when more CPU / memory is needed
- Apache as Reverse Proxy
  - Only sends requests to backend servers
  - The thread will be blocked until response is returned
    - which will send to client
  - Load enterily on memory for lots of connections
    - It will increase the thread pool size / 1 thread per client
  - We can only scale Apache as LB only vertically / **poor design**
 

![Apache Webserver](assets/images/93.png)

Good option as a WebServer for dynamic webpages

---



