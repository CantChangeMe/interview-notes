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
