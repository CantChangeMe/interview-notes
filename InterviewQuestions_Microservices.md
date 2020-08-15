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
    
    
#### 6.What is Spring Cloud?
  Spring Cloud provides tools for developers to quickly build some of the common patterns in distributed systems 
  (e.g. configuration management, service discovery, circuit breakers, intelligent routing, leadership election, distributed sessions, cluster state).
  
#### 7.What problems are solved by Spring Cloud?
  While developing distributed microservices with Spring Boot we face few issues which are solved by Spring Cloud.

**The complexity associated with distributed systems** – This includes network issues, Latency overhead, Bandwidth issues, security issues.
**Ability to handle Service Discovery** – Service discovery allows processes and services in a cluster to find each other and communicate.
**Solved redundancy issues** – Redundancy issues often occur in distributed systems.
**Load balancing** – Improves the distribution of workloads across multiple computing resources, such as a computer cluster, network links, central processing units.
**Reduces performance issues** – Reduces performance issues due to various operational overheads.

#### 8.What is the use of WebMvcTest annotation in Spring MVC applications?
  @WebMvcTest annotation is used for unit testing Spring MVC Applications in cases where the test objective is to just focus on Spring MVC Components.Like testing the controller   ToTestController. All other controllers and mappings will not be launched when this unit test is executed.
  
#### 9.What do you understand by Distributed Transaction?
  Distributed Transaction is any situation where a single event results in the mutation of two or more separate sources of data which cannot be committed atomically. In the        world of microservices, it becomes even more complex as each service is a unit of work and most of the time multiple services have to work together to make a business            successful.
  
#### 10.What is an Idempotence and where it is used?
  Idempotence is the property of being able to do something twice in such a way that the end result will remain the same i.e. as if it had been done once only.
  Usage: Idempotence is used at the remote service, or data source so that, when it receives the instruction more than once, it only processes the instruction once.  
#### 11.What is Two Factor Authentication?
      Login+OTP
      
#### 12.What are Client certificates?
A type of digital certificate that is used by client systems to make authenticated requests to a remote server is known as the client certificate. Client certificates play a very important role in many mutual authentication designs, providing strong assurances of a requester’s identity.      

#### 13.What is OAuth?
OAuth stands for open authorization protocol. This allows accessing the resources of the resource owner by enabling the client applications on HTTP services such as third-party providers Facebook, GitHub, etc. So with this, you can share resources stored on one site with another site without using their credentials.

#### 14.What is the use of Container in Microservices?
Containers are a good way to manage microservice based application to develop and deploy them individually. You can encapsulate your microservice in a container image along with its dependencies, which then can be used to roll on-demand instances of microservice without any additional efforts required.
   Container image = Microservice + Code library

#### 15.What is the purpose of Docker?
**Docker** provides a container environment that can be used to host any application.
In this, the **software application** and **the dependencies which support it** are tightly-packaged together.
So, this **packaged product** is called **a Container** and since it is done by Docker, it is called **Docker container**!

#### 16.What do you mean by Continuous Integration (CI)?
Continuous Integration (CI) is the process of automating the build and testing of code every time a team member commits changes to version control. This encourages developers to share code and unit tests by merging the changes into a shared version control repository after every small task completion.

#### 17.What are Reactive Extensions in Microservices?
Reactive Extensions also are known as Rx. It is a design approach in which we collect results by calling multiple services and then compile a combined response. These calls can be synchronous or asynchronous, blocking or non-blocking. Rx is a very popular tool in distributed systems which works opposite to legacy flows.
