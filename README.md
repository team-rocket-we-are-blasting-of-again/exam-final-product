# System Integration Exam Project, Cphbusiness SOFT Fall 2022     
  
## System solution for MTOGO A/S :computer:    

## Group Members :wave:     

- Frederik Johnsen, cph-fj111@cphbusiness.dk
- Jean-Poul Leth-Møller, cph-jl360@cphbusiness.dk
- Mathias Parking, cph-mp525@cphbusiness.dk
- Magdalena Wawrzak cph-mw216@cphbusiness.dk
- Tobias Zimmermann cph-tz11@cphbusiness.dk

### Table of content
1. [Introduction](#Introduction)
2. [Repositories](#Repositories)
3. [Getting-started](#Getting-started)
   1. [Environments](#Environments)
   2. [How to use the project](#How-to-use-the-project)
4. [Legacy system](#Legacy-system)
5. [Business cases](#Business-cases)
6. [Functional requirements](#Functional-requirements)
7. [Design and diagrams](#Design-and-diagrams)
   1. [Domain models](#Domain-models)
   2. [C4 models](#C4-models)
   3. [Diagrams](#Diagrams)
8. [Architecture](#Architecture)
9. [System integration patterns](#System-integration-patterns)
10. [Technologies](#Technologies)
11. [Mandatory feature requirements](#Mandatory-feature-requirements)
12. [Version history](#Version-history)
13. [Reflection](#Reflection)
     
### Introduction     
MTOGO A/S is seeking to replace its current system since it is now insufficient. The reasoning behind this is because the old system is monolithic in architecture. As MTOGO is growing internationally as a business, they need to future proof their business by becoming scalable and reliable in multiple locations.
  
also link to our video here
also link to our deployment here  

### Repositories
The following is a list of all the current and future github repositories that was used to develop the MTOGO Food Delivery System.

#### Microservices
1. Customer Service: https://github.com/team-rocket-we-are-blasting-of-again/exam-customer-service
2. Order Service: https://github.com/team-rocket-we-are-blasting-of-again/exam-order-service
3. Courier Service: https://github.com/team-rocket-we-are-blasting-of-again/exam-courier-service
4. Restaurant Service: https://github.com/team-rocket-we-are-blasting-of-again/exam-restaurant-service
5. Authentication Service: https://github.com/team-rocket-we-are-blasting-of-again/exam_auth_service
6. Payment Service: https://github.com/team-rocket-we-are-blasting-of-again/exam-payment-service
7. Notification Service: https://github.com/team-rocket-we-are-blasting-of-again/exam-notification-service
8. API Gateway: https://github.com/team-rocket-we-are-blasting-of-again/exam-api-gateway
9. Camunda Server: https://github.com/team-rocket-we-are-blasting-of-again/exam-camunda-server

#### DevOps
1. Gateway Subscription: https://github.com/team-rocket-we-are-blasting-of-again/exam-gateway-subscription
2. GitOps: https://github.com/team-rocket-we-are-blasting-of-again/exam-gitops
3. Prebuilt Images: https://github.com/team-rocket-we-are-blasting-of-again/exam-prebuilt-images
4. [Docker Hub](https://hub.docker.com/u/tobiaszimmer)

#### Legacy System
1. Legacy Code: https://github.com/team-rocket-we-are-blasting-of-again/exam-legacy-system
2. Legacy Translator: https://github.com/team-rocket-we-are-blasting-of-again/exam-legacy-translator


#### Frontend
1. Frontend Client: https://github.com/team-rocket-we-are-blasting-of-again/exam-client
2. Restaurant Client: https://github.com/team-rocket-we-are-blasting-of-again/exam-restaurant-client
3. Transaction Client: https://github.com/team-rocket-we-are-blasting-of-again/exam-transaction-client

### Other
1. Payment Processor: https://github.com/team-rocket-we-are-blasting-of-again/exam-payment-processor
2. Payment Validator: https://github.com/team-rocket-we-are-blasting-of-again/exam-payment-validator
3. Transaction Service: https://github.com/team-rocket-we-are-blasting-of-again/exam-transaction-service

### Getting started  
In order to run this application locally it is required to have docker deamon installed and running. We recommend using Docker desktop.


#### Environments
The whole system can be run as docker components with whe command runned from root of this directory :


* ```shell
    docker-compose up -d
    ```  
  
#### How to use the project  

Once the docker container is up and runnig, verify if the auth-, restaurant-, courier- and customer-services have subscribed to the gateway api by calling ``localhost:9999/gateway/route``. Response should contain 6 JSON-objects.

To access the services, use this:
[Local Postman collection](https://github.com/team-rocket-we-are-blasting-of-again/exam-final-product/blob/main/MTOGO.postman_collection.json)  

### Legacy system  
Analyze the domain and identify potential problems in existing legacy digital systems at the 
customer, such as lack of functionality, performance issues, operation difficulties, data 
storage and transformation issues, customer dissatisfaction, etc.    
    
### Business cases
MTOGO A/S wants to expand their current operations by implementing a new system which can handle a higher workload and is able to be distributed internationally. The new system will focus on three main types of users - customers, restaurants, and couriers.

They will be able to make an account in order to use the system. The customers can order food either through the web or a mobile application. The restaurants sign up as food providers either by using the MTOGO API or using the MTOGO provided restaurant application. The couriers can sign up through the MTOGO courier application where they select regions and orders. A courier is viewed as an employee and will be paid based on the amount of orders they deliver.

Restaurants pay a fee to MTOGO for using their service and a variable share of the total order value before VAT. The order fee varies from a minimum of 3%, for orders over a 1000 DKK, to a maximum of 6%, for orders under 100 DKK. Each restaurant specifies the minimum order size for delivery. Customers of MTOGO will have to pay a delivery fee.

Payment will be reserved when a customer makes an order. Customers will pay automatically once a restaurant has completed an order and a courier has delivered their order. Through the MTOGO application customers will be able to track their order through the delivery phase which include preparation and delivery. 

Additionally MTOGO management will be able to view all orders in the system through an administration dashboard. Likewise restaurants will be able to view all their orders in a dashboard. All orders will either be accepted or declined by the restaurant. 

  
### Requirement specification
#### Non-Functional

NFR1: The system must be made using a microservice architecture, so as to decouple the services and make the system modular. Making it easier to maintain, test and deploy each service separately.

NRF2: The system must use orchestration and container technology, so that the system becomes easily scalable with high availability, on an international scale.

NFR3: The system must make use of an event driven architecture.

NFR4: 	The development team must make use of DevOps practices, such as automatic testing, being agile, and generally providing fast deliveries.

NFR5: The system must be tested thoroughly before going into production, by using a pre production environment.

NFR6: The system must be GDPR compliant.

NFR7: The system must have low response times in all supported markets.

NFR8: The system must have backups of stored data, such that the data will not be lost in the event of database failure.

#### Functional

General Requirements :

R1: MTOGO requires no data loss when migrating to the new system.

Restaurant requirements:

R2: Restaurants should be able to integrate with the MTOGO system.

R3: Restaurants of both big and small sizes should be supported, by allowing small businesses to use an interface for order management system provided by MTOGO, and allowing big businesses to integrate with an API that we expose to them. The system should allow restaurants to view orders, accept or decline orders, and see analytics on their previous orders.

Customer requirements:

R4: Customers should be able to order food from any of the restaurants that have an integration setup with the MTOGO system provided they are not too far away.

R5: Customers must be able to search for restaurants, through various search criteria, such as restaurant name, food type etc. given that the restaurants are within a certain distance from the customer.

R6: Customers must be able to provide feedback on the courier. This should be feedback on speed of delivery, and general quality of service.

R7: Customers must be able to provide feedback on the restaurant. This should be feedback on quality of food, and interactions with the customer.

R8: Customers must receive notifications about their orders’ status in the app. A customer is notified when their order is being prepared, when a delivery estimate is made, when the order is being delivered, when the order has been delivered and when the order is canceled for any reason.

R9: Customers must be recommended restaurants in the app based on their location, any current events, feedback given to restaurants, customers’ previous orders and food preferences.

R10: Customers must receive an email containing a receipt of any order they make.

R11: Customers have access to a profile where they can see all relevant data about themselves. This includes previous orders, coupons and general information.

R12: Customers are able to register and login to the system in order for them to make orders and have a profile.

Payment requirements:

R13: MTOGO does not want to deal with payments themselves, so that they do not get problems with authorities. This will also make it easier to have a payment system that works internationally.

R14: Restaurants must pay a fee to MTOGO for using the MTOGO system.

R15: Delivery fees for customer orders are calculated on order, and are visible in the order receipt.

R16: In order for a courier to get paid for each delivery, the system calculates reward per order by the basic reward , busy hours factor and distance as shown in the table. The distance reward is counted after first 2000 m

Courier requirements:

R17: A person must be able to sign in as a courier.

R18: Courier must be able to choose to go online in order to be able to pick up orders.

R19: Courier must be able to choose one area to work within.

R20: Courier must be able to see delivery tasks available to be picked up from restaurants.

R21: Courier must be able to see information about pickup and drop off (locations of both the restaurant and the customer, live updates on pickup and delivery time, task distance).

R22: Courier must be able to provide transportation type in order to estimate delivery time

R23: Courier must be able to claim an order to pick up.

R24: Courier must be able to check all items of the order that is being picked up at the restaurant and approve it.

R25: Courier must be able to set the order as delivered to the customer if the courier is within 500 m from the delivery destination.

R26: Courier must be able to cancel the claimed order pickup by providing the cancelation reason to the area manager.

R27: Courier must be able to view his/hers  stats by current day, week, month or by custom settings. 

R28: A person must be able to sign up as a courier.

Management requirements:

R29: Managers are able to view a dashboard of orders which will contain information about all orders in the system. 

R30: If, for any reason, orders are not chosen by couriers to deliver within 5 minutes, then the manager will get a notification about the order.
  
### Design and diagrams
The design of the system was done using the DDD and C4 modeling approaches. The design that was developed had to be visualized for a better understanding overall. The given requirements also produced some diagrams.
The main artifacts and diagrams that has come from this process include the following:

1. Architectural diagram
2. DDD Domain Model
3. DDD Context map
4. Event Storming Drawing
5. Context diagram - C4 level 1
6. Container diagram - C4 level 2
7. Component diagram - C4 level 3
8. Use Case Diagrams
9. Sequence Diagrams
  
#### Domain models 
Domain Driven Design

The domain model that was produced from the DDD process gives an overview of the domain as it was defined during initial phases of development.

![DDD - Domain Model](/images/domain-model.png)

This is the initial domain model, where the subdomains were identified. There is, notably, a large amount of subdomains, which is why the team decided to focus in on a few core subdomains in order to meet the deadline, namely the Customer, Courier, Restaurant, and Order subdomains, as these were deemed the most central parts of the system.

The following is the DDD Context Map.

![DDD - Context Map](/images/context-map.png)

This is the context map that was made following the domain model. Here the previously identified subdomains have been placed into contexts, and relationships have been drawn between them. The Notification, Location, and Search subdomains were identified as being useful in several different contexts, and were placed on the map as shared kernels. Also present are lines between contexts, showing the relationships between the different contexts, by designating an upstream and a downstream in the relations.
  
#### C4 models  
The team has made several domain models of different level of the C4 model. The first being the context level.

![C4 - Context Model](/images/MTOGO_level1.JPG)

The diagram shown in the above figure was mainly used to deepen the understanding of the system context, the actors, and the external systems that would need to be integrated. The legacy system of the MTOGO business is also shown here and how it’s supposed to integrate with the new system. The new MTOGO system was made using a microservice architecture, and by using the Container diagram of the C4 model, they could visualize how the different services would communicate.

A Container diagram for each actor and their respective sub-contexts, was also made.

![C4 - Container Model](/images/Courier_Level2.png)

This diagram is meant to visualize the services that are integrated with any actions made by a courier user. This diagram was made to visualize what services would need to be made in order for the system to be optimally functional.

The last C4 model that was drawn for purposes of explaining the subsystems and architecture is level 3 visualizing the Order Service.

![C4 - Component Model](/images/OrderServicelvl3.png)

The third level of the C4 model is meant to describe the components used in each container. The Component diagram in the above figure was made later in the process, as this would allow us to make a more precise model of what components the service would have.

The forth level of the C4 diagram has not been made by the team, as the team did not see any utility in it.
  
#### Sequence Diagram  
-class diagrams MISSING 

The communication between each microservice in the courier context is shown by the connector arrows in the level 2 figure from earlier, but they don’t explain much about what actions are made or how they happen. To explain the details of one of these transactions, the team has used a sequence diagram. Specifically the use case of couriers having delivery tasks displayed to them.

![Sequence Diagram 1](/images/Sequence_Displaying_available_delivery_tasks.png) 
  
### Architecture
Short aboout our thoughts and why we went with the current solution (has to include microservice structure and event driven structure)  
-insert overview of the whole system architecture  
-insert example of our microservice package structure (maybe explain here why we went with hexogonal and the four layers)  

![Architecture](/images/Architecture.png) 

![Service architecture](/images/folder-structure.png) MISSING 
  
### System integration patterns
The Enterprice Integration patters that has been made use of throughout this project are the following:

- Publish-Subscribe Channel
- Request-Reply
- Process Manager
- Polling Consumer
- Message Broker
- Remote Procedure Invocation
- Pipes and Filters
- Message Channel	
- Channel Adapter
- Message Translator	
- Message Endpoint	
- Message	
- Event-Driven Consumer	
- Format Indicator
  
### Technologies  
The following is a list of the used technologies:  
    
#### Java  
* Java 17 
* Spring boot 2.7.5 
* Junit 5.8.1 
* grpc 1.49.2 
* Surefire 2.22.2 
* pitest 1.9.6 
* mockito 4.3.1   
  
#### Rust  
* Rust 1.67-nightly 
* Cargo-mutants 1.2.0 
* Tarpaulin 0.22.0 
* Rocket 0.5.0-rc.2 
* Tokio 1.0.0 
* Tonic 0.8.2  
  
#### Database  
* Postgresql 15.1
* redis:6.2-alpine

#### Other
* kafka 3.3.1
* kubernetes 2.13.1
* camunda 7
    
### Mandatory feature requirements  
The following is a checklist from Dora which are requirements which we HAVE to meet so we will use this as a check list and write very short  
how we met each of the requirements. 
     
The software system integrates a variety of disparate applications, components, and data sources
of three types: 
  
It Is a Composite System   
a. monolithic or legacy application  
b. web services or service-oriented application  
c. microservices architecture application  
  
It Has Business Context  
The integration architecture design reflects the business context:  
a. implements domain-driven design  
b. applies BPM approach  
c. implements enterprise integration patterns  
d. enables storage, integration and transformation of various data sources  
  
Solution Applies Integration Technologies  
The development implements a variety of integration and communication techniques introduced 
in class, such as:  
a. APIs and API Gateways  
b. SOA and MOM  
c. data and event streaming platforms  
d. process automation platforms  
e. microservices composition, discovery, and management tools  
  
Solution Implements Quality Standards and Best Practices  
The product illustrates implementation of  
a. integration standards  
b. decoupling and configuration of components  
c. synchronous and asynchronous interaction styles  
d. best use of network technologies and Internet  
e. object-oriented programming, variety of programming languages and development 
platforms  
You can consider the Twelve-Factor App recommendations.  
  
Client Applications  
There is no specific requirement for developing client applications.  
a. publicly available instruments, such as Postman, curl, console CLI, and web browsers, 
which provide a simple interface for illustrating the functionality of the integrated system 
can be used instead  
  
Documentation  
There is no requirement for writing report. Instead, the team is expected to add  
a. in the GitHub repository, a .md file, in which the integration development process and 
considerations are briefly explained and visualized by diagrams. Including an 
architectural diagram of the whole system and its components is a must.  

b. in Wiseflow, a 10-minute video, where the business cases, problems and solutions
are discussed, demonstrated, and evaluated by the team members  
  
  
### Version history  
Version history from initial build to release:  

- 0.0.1 initial start
- 0.0.3 removal of bugs and optimization
- 1.0.0 release to production  
  
### Reflection  
We can reflect over the things we have made or what could have been made here.  
  



   
 




