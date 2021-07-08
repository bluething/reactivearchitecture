## API Gateway Pattern

#### The problem

- How do the clients of a Microservices-based application access the individual services?  
- Does the client have to fetch data from numerous services?  
- Different clients need different data. How our services provide it all?  
- Network performance is different for different types of clients. How our services satisfy them all in terms of performance? Does our services need to aware about how each client interact with them?  
- The number of service instances, and their locations (host+port) changes dynamically. Does the client have to pay attention to this?  
- Partitioning into services can change over time and should be hidden from clients.  
- Services might use a diverse set of protocols, some of which might not be web friendly.

#### The solution

![api gateway](https://github.com/bluething/reactivearchitecture/blob/master/images/apigateway.jpg?raw=true)

The API gateway handles requests in one of two ways.  
1. Some requests are simply proxied/routed to the appropriate service.  
2. It handles other requests by fanning out to multiple services.

There are variation for this pattern  
![backend for frontend](https://github.com/bluething/reactivearchitecture/blob/master/images/backendforfrontend.png?raw=true)

#### The benefit

1. Insulates the clients from  
   - How the application is partitioned into microservices.  
    - How to determine the locations of service instances
2. Provides the optimal API for each client.  
3. Reduces the number of requests/roundtrips.  
4. Simplifies the client, from call multiple service into one call to the gateway.  
5. Translates from a “standard” public web-friendly API protocol to whatever protocols are used internally.

#### What to consider?

- How implement the API gateway?  
- Increased complexity. Because the API gateway is yet another moving part that must be developed, deployed and managed.  
- Increased response time due to the additional network hop through the API gateway. However, for most applications the cost of an extra roundtrip is insignificant.

#### Reference

[Pattern: API Gateway / Backends for Frontends](https://microservices.io/patterns/apigateway.html)