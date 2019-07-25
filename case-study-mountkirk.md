# Mountkirk Games

- mobile games maker
---
- current mobile game not scaling well
- new game (hosted on GPC) needs to scale well

> Their current model is to write game statistics to files and send them through an ETL tool that loads them into a centralized MySQL database for reporting.

## Goals

- build new game, greenfield env
- two key environments
    - game backend on GCE
        - hardened linux distro
        - **NoSQL transactional** DB *datastore/firestore*
    - separate analytics setup
    - different storage device for each

## What do they care about

- scaling
- measuring performance
- reliable experience for users - no downtime
- managed services
- analytics - usage patterns
- global footpring

## Business reqs

- Increase to a global footprint
    - multi-regional instance group backends fronted by HTTP LB
    - multi-regional ingest/storage options
        - Pub/Sub, Datastore, BigQuery, Cloud Storage
- Improve uptime - downtime is loss of players
    - autoscaling instance groups
    - global LB
    - pub/sub, dataflow accounts for slow/late data
    - pub/sub buffers data, no scaling cap, no log backlog
- Increase efficiency of the cloud resources we use
    - scaling
    - stackdriver monitoring
- Reduce latency to all customers
    - multi-regional setup, CDN, datastore?

## Tech reqs

### Requirements for Game Backend Platform

- Dynamically scale up or down based on game activity.
    - autoscaling MIGs
    - stackdriver to measure performance/efficieny
        - drive autoscaling
- Connect to a transactional database service to manage user profiles and game state.
    - datastore/firestore - noSQL transactional DB
- Store game activity in a timeseries database service for future analysis.
    - store in BigQuery
    - BigQuery/Bigtable
        - bigtable ms response time, BQ response measured in seconds, scale more efficiently
        - no requirement for low latency analytics response time
- As the system scales, ensure that data is not lost due to processing backlogs.
    - LB, MIGs, pub/sub
- Run hardened Linux distro.
    - custom images in MIGs

### Requirements for Game Analytics Platform

- Dynamically scale up or down based on game activity.
- Process incoming data on the fly directly from the game servers.
    - stream data to pub/sub -> dataflow -> warehouse
- Process data that arrives late because of slow mobile networks.
    - stream data to pub/sub -> dataflow -> warehouse
- Allow queries to access at least 10 TB of historical data.
    - BigQuery
- Process files that are regularly uploaded by users’ mobile devices.
    - upload to cloud storage
    - process via dataflow
