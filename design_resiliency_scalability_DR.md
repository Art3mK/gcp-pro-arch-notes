# Design for Resiliency, Scalability and DR

- Resiliency is the quality of a design that accounts for and handles failure

## Failure due to loss

- don't depend on hw
- sw: modularize, monitor, test, canary
- ppl: review procedures, escalate
- comms: don't assume it happened
---
- anticipate failure
- design for failure
- fail gracefully

### SPOF

- hw, network, data
    - replicate everything \o/
- design to avoid SPOFs
    - A spare spare, N+2
    - plan to have one unit out for upgrade and survive another failing
    - don't make any single unit too large
    - don't concentrate responsibility into a single process or server
    - try ot make units interchangeable clones

### Correlated failures

Correlated failures occur when related itmes fail at the same time.

the group of related items that cloud fail at one time is __failure domain__

design to avoid correlated failures:
- decouple servers, use microservices
- divide business logic into services based on failure domains
- split responsibility into components and spread over multiple processes
- separate and isolate the risks
- design independent but collaborating services

## Failure due to overload

overload failure is when a resources crosses into non-linear behaviour -> crash, thrash, stop responding, or break adjacent resources that service depends on

- prevention is the best strategy
- monitor "safety" size
---
- queries of death
    - monitor query performance iteratively
    - ensure notifications of these issues gets back to the developers
- retries, logarithmic backoff, BGP route dampening as example

### Detecct overload

- early warning systems (canaries)

## Coping with failures/DR

- the time to prepare for an emergency is before it happens
- no surprises!
----
data integrity:
- lazy deletion -> trash -> soft-deletion -> hard-deletion -> data is gone/backups
- the goal isn't backup or archive, it is __restore__.
    - periodic testing
    - automating restore from backup
    - incorporate recovery testing into your desing


## Scalable and resilient design

- use health checks to monitor instances
- automatically replace instances that have failed or become unavailable
    - understand its role in the system
    - automatic configuration
    - discover any of its deps
    - start handling reqs automatically
- state storage
    - cloud storage
    - cloud SQL
- network
    - LBs
