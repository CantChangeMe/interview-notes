# Microservices Interview Questions

#### 1.What are advantages of Microservices Architecture?
  |Advantage|	Description|
  |---------|-------------
  |Independent Development|	All microservices can be easily developed based on their individual functionality|
  |Independent Deployment|	Based on their services, they can be individually deployed in any application|
  |Fault Isolation|	Even if one service of the application does not work, the system still continues to function|
  |Mixed Technology Stack|	Different languages and technologies can be used to build different services of the same application|
  |Granular Scaling|	Individual components can scale as per need, there is no need to scale all components together|
  

#### 2.What are the best practices to design Microservices?
  1.Separate data store for each microservice.
  2.Separate build for each microservice.
  3.Deploy into containers.
  4.Treat server as stateless.
  
#### 3.How does Microservice Architecture work?  
  **Clients** – Different users from various devices send requests.
  
  **Identity Providers** – Authenticates user or clients identities and issues security tokens.
  
  **API Gateway** – Handles client requests.
  
  **Static Content** – Houses all the content of the system.
  
  **Management** –  Balances services on nodes and identifies failures.
  
  **Service Discovery** – A guide to find the route of communication between microservices.
  
  **Content Delivery Networks** – Distributed network of proxy servers and their data centers.
  
  **Remote Service** – Enables the remote access information that resides on a network of IT devices.

#### 4.Cons of Microservice Architecture?
    1.Increases troubleshooting challenges
    2.Increases delay due to remote calls
    3.Increased efforts for configuration and other operations
    4.Difficult to maintain transaction safety
    5.Tough to track data across various boundaries
    6.Difficult to code between services

#### 5.Monolithic vs SOA vs Microservices
    Monolithic - Signle Unit
    SOA - Coarse-grained
    Microservices - fine-grained
    
    
#### What is Spring Cloud?
  Spring Cloud provides tools for developers to quickly build some of the common patterns in distributed systems 
  (e.g. configuration management, service discovery, circuit breakers, intelligent routing, leadership election, distributed sessions, cluster state).
  
#### What problems are solved by Spring Cloud?
  While developing distributed microservices with Spring Boot we face few issues which are solved by Spring Cloud.

**The complexity associated with distributed systems** – This includes network issues, Latency overhead, Bandwidth issues, security issues.
**Ability to handle Service Discovery** – Service discovery allows processes and services in a cluster to find each other and communicate.
**Solved redundancy issues** – Redundancy issues often occur in distributed systems.
**Load balancing** – Improves the distribution of workloads across multiple computing resources, such as a computer cluster, network links, central processing units.
**Reduces performance issues** – Reduces performance issues due to various operational overheads.

