### How to prevent a network or service failure from cascading to other services?

![circuit breaker](https://github.com/bluething/rectivearchitecture/blob/master/images/circuitbreaker.png?raw=true)

When one service synchronously invokes another there is always the possibility that the other service is unavailable or is exhibiting such high latency it is essentially unusable.  
Precious resources such as threads might be consumed in the caller while waiting for the other service to respond.  
This might lead to resource exhaustion, which would make the calling service unable to handle other requests. The failure of one service can potentially cascade to other services throughout the application.

#### Reference:

[Pattern: Circuit Breaker](https://microservices.io/patterns/reliability/circuit-breaker.html)  
[CircuitBreaker](https://martinfowler.com/bliki/CircuitBreaker.html)