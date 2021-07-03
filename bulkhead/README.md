## Bulkhead Pattern

#### The story

The bulkhead pattern is based on a concept from building ships. With a bulkhead design, a ship is divided into completely segregated and watertight compartments called bulkheads.  
Even if the ship’s hull is punctured, because the ship is divided into watertight compartments (bulkheads), the bulkhead will keep the water confined to the area of the ship where the puncture occurred and prevent the entire ship from filling with water and sinking.

#### The problem

The same concept can be applied to a service that must interact with multiple remote resources. Excessive load or failure in a service will impact all consumers of the service.  
a consumer may send requests to multiple services simultaneously, using resources for each request.  
When the consumer sends a request to a service that is misconfigured or not responding, the resources used by the client's request may not be freed in a timely manner. As requests to the service continue, those resources may be exhausted.  
For example, the client's connection pool may be exhausted. At that point, requests by the consumer to other services are affected.  
Eventually the consumer can no longer send requests to other services, not just the original unresponsive service.

#### The solution

Partition service instances into different groups, based on consumer load and availability requirements.  
A consumer can also partition resources, to ensure that resources used to call one service don't affect the resources used to call another service.

#### The benefit

1. Isolates consumers and services from cascading failures.  
2. Other services and features of the application will continue to work.  
3. Allows you to deploy services that offer a different quality of service for consuming applications. A high-priority consumer pool can be configured to use high-priority services.

#### What to consider?

- Define partitions around the business and technical requirements of the application.  
- Consider the level of isolation offered by the technology as well as the overhead in terms of cost, performance and manageability.  
- Consider combining bulkheads with _retry_, [_circuit breaker_](https://github.com/bluething/reactivearchitecture/tree/master/circuitbreaker), and _throttling_ patterns to provide more sophisticated fault handling.  
- When partitioning consumers into bulkheads, consider using _processes_, _thread pools_, and _semaphores_.  
- When partitioning services into bulkheads, consider deploying them into separate virtual machines, _containers_, or processes.  
- Services that communicate using asynchronous messages can be isolated through _different sets of queues_. Each queue can have a dedicated set of instances processing messages on the queue, or a single group of instances using an algorithm to dequeue and dispatch processing.  
- Determine the level of granularity for the bulkheads. For example, if you want to distribute tenants across partitions, you could place each tenant into a separate partition, or put several tenants into one partition.  
- Monitor each partition’s performance and SLA.

#### When to use this pattern?

- Isolate resources used to consume a set of backend services.  
- Isolate critical consumers from standard consumers.  
- Protect the application from cascading failures.

#### When to avoid this pattern?

- Less efficient use of resources may not be acceptable in the project.  
- The added complexity is not necessary

#### Reference

John Carnell. 2017. _Spring Microservices in Action_ (1st. ed.). Manning Publications Co., USA.  
[Bulkhead pattern](https://docs.microsoft.com/en-us/azure/architecture/patterns/bulkhead)  
[Implementing Bulkhead with Resilience4j](https://reflectoring.io/bulkhead-with-resilience4j/)