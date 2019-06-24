# Design and Process

State/Measurement/Requirements

## Defininig a service

Rough -> Structured desing (+iterate) -> Measurable

- Presentation layer (networking)
- Business logic layer (compute)
- Data layer (storage)
- Scalability/Reliability/Availability/DR/Resiliency
- Security/Privacy/Denial of Service
- capacity/cost optimization
- launching/monitoring/alerting/responding

### state and solution

- the best state is no state
- the worst case for state is a hotspot
- push state off of the actual services that are handling and relying on states, so you push them to a back-end
    - stateless frontends
    - separate read and write paths
    - caching of the read path
    - push stateful servers lower in the stack
- distributing state
    - > latency
    - replication
    - split-brain situations

### measurement

- Service Level Indicators (SLI)
    - availability of a web page
    - how fast the system responds when a user clicks a button
    - directly observable and measurable by the users
    - not an internal metric
    - not all statistics should be SLIs
    - represents the users' experience
    - reliably represent the health of the system
    - gold monitoring signals: latency/traffic/errors/saturation (resource usage)
- Service Level objective (SLO)
    - threshold of pain
    - threshold value for an SLI, lowest/poorest level of service
- Service Level Agreement (SLA)

Not all services have an SLA, but all services should have an SLO.

### requirements

- qualitative requirements
    - why is the system needed or desired? What problem does it solve?
    - who are stakeholders and who are the users? What do they care about and not care about
    - who is developing this? What is in scope? What is feasible and what is not feasible?
    - what does the system need to do? What are the priorities, required versus nice-to-have?
    - when do the users need and/or want the solution? Are there any time/value tradeoffs?
- quantitative reqs
    - time
        - operational time constraints
        - cost of downtime
    - data
        - cost of data cost
        - data volume
        - throughput
        - freshness
        - groups of data
    - users
        - number of users
        - location of users
- scaling reqs
    - what will limit your ability to grow your app
    - which resource constraints are important to pay attention to? state? Data storage? Frontend?
    - how can you design to push past these limits when necessary?
    - growth in scale tends to be iterative and new solutions need to be found as scale issues arise
- size requirements
    - what factors are importatnt to the size of the solution
    - dimensions/replication/rate of change

## Business-logic layer

### Microservices arch

Small modular services, each service is going to contribute to some individual business goal
- atomic, single-purpose code is easier to develop and maintain
- does one thing and does it very well
- supports A/B testing

Independenlty developed services aid in:
- faul isolation
- debugging
- redundancy and resiliency

but:
- unit testing is easier, integration testing is harder.
---
- microservices makes sense when there are many consumers of an atomic unit of functionality
- doesn't make sense for one consumer of tightly-coupled functionality

GCP options:
- cloud functions
    - node.js
    - not a low latency service
    - there are few resources that can be adjusted for price/performance tradeoffs
- GAE
    - full code isolation
    - many languages
    - HTTP/RESTful API
    - 60s session timeout in standard
    - cons:
        - shared services that must be isolated in the app design
        - one master app per project
        - multiple apps incur additional overhead
        - no local FS access
---
### Horizontal scaling design

N+3 (N/3) query per second per backend server

- keep server simple, do one thing well
- minimize complexity
- constuct simple and concise APIs
- identify where tasks are separable
- split into separata servers
---
prefer small, stateless servers
- easy to scale, no state to shard/rebalance
- failure is cheap, no state to migrate/recover
- easy to LB, no hot-spotting

## Data layer design

- data persistent mechanism
    - database services
    - storage services
- data access layer

### Classifying and characterizing data

- data integrity

**data transaction** properties (CAP), choose two:
- consistency
- availability
- partition tolerance

consistency + PT = ACID (atomicity, consistency, isolation, durability)
availability + PT = BASE (basically available, soft state, eventual consistency)

optimizing:
- uptime
- latency
- scale
- velocity
    - how fast service will grow
- privacy

## Presentation layer
